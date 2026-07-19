---
id:
  - CASO-182
link: https://www.youtube.com/watch?v=MBfrSKjoiRA
setor:
  - Suporte
  - Implementação
  - Operacional
modulo:
  - Hotelaria / Controle de Hospedagem
tags:
  - hotelaria
  - reservas
  - check-in
  - check-out
  - calculo-de-periodo
  - multas
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Módulo de Hotelaria]]
2. [[#Ciclo de Vida da Hospedagem (Status)]]
3. [[#Controle de Ocupação e Disponibilidade Futura]]
4. [[#Faturamento e Regras de Cálculo de Período]]
5. [[#Lógica de Aplicação de Multa por Estouro]]
6. [[#Pontos Críticos e Roadmap do Módulo]]

# Visão Geral do Módulo de Hotelaria
O módulo de **Hotelaria** gerencia o ciclo completo de permanência de clientes em acomodações (apartamentos ou quartos), oferecendo suporte tanto para o modelo tradicional de diárias quanto para a locação fracionada por faixas de horários (períodos). O sistema centraliza o mapeamento de reservas, o registro de múltiplos hóspedes com placas de veículos para controle de portaria, o cálculo automatizado de permanência e a integração com o [[PDV]] para fechamento financeiro.

# Ciclo de Vida da Hospedagem (Status)
A acomodação transita por três estados principais refletidos de forma visual na grade de monitoramento do sistema:

*   **Reservado:** Representa uma intenção de compra para uma data futura, onde a acomodação fica bloqueada no calendário para novos agendamentos, mas permanece livre para ocupação imediata no presente.
*   **Ocupado:** Acionado no momento em que o cliente realiza a entrada física. A acomodação passa a contabilizar o tempo de permanência ativa.
*   **Liberado:** Status redefinido após o encerramento do processo de saída e quitação total dos débitos no caixa, disponibilizando o quarto para a próxima alocação.

# Controle de Ocupação e Disponibilidade Futura
A interface do sistema exibe em paralelo a situação em tempo real do quarto e a sua agenda futura. Isso permite que um quarto que esteja atualmente com o status de `Ocupado` receba uma marcação de `Reservado` para datas subsequentes.

### Processo de Check-in (Entrada)
1.  Na grade de mapas de quartos, selecione a reserva correspondente.
2.  Clique no botão **Chegada** (ou Alterar). O sistema preenche de forma automática e imutável os campos de data e hora atuais.
3.  Acesse o bloco de **Controle de Hóspedes** para listar todas as pessoas que ocuparão o ambiente. É possível vincular dados como nome e placa do veículo para triagem de segurança.
4.  Clique em **Salvar**. O status da acomodação é atualizado imediatamente para `Ocupado`.

# Faturamento e Regras de Cálculo de Período
No momento do encerramento da estadia, o operador dispara o processo clicando no botão **Saída**, fazendo com que o sistema registre o horário corrente e efetue o cálculo do valor devido baseado no tipo de parametrização da acomodação.

### Cenário Prático sem Aplicação de Multa (Regra por Período Cheio)
*   **Configuração do Quarto:** Locação parametrizada em frações de 3 em 3 horas pelo valor de R$ 9,00.
*   **Horário de Chegada:** 15:00h
*   **Horário de Saída:** 20:00h
*   **Tempo Total Calculado:** 5 horas de permanência.

```json
{
  "calculo_periodo_hotelaria": {
    "hospedagem_id": 932,
    "regra_faixa_horas": 3,
    "valor_por_faixa": 9.00,
    "horas_consumidas": 5.0,
    "periodos_faturados": 2,
    "motivo_periodos": "5 horas extrapolam 1 período (3h), forçando a cobrança de 2 períodos cheios na ausência de multa fracionada",
    "valor_total_hospedagem": 18.00
  }
}

Na ausência de uma regra de multa configurada, o sistema arredonda a fração excedente para cima. Como as 5 horas consumidas superam o primeiro limite de 3 horas, o mecanismo computa **2 períodos inteiros**, totalizando **R$ 18,00** no fechamento do documento.

# Lógica de Aplicação de Multa por Estouro

Para estabelecimentos que optam por não cobrar um período cheio caso o cliente ultrapasse o limite por poucos minutos, o sistema permite configurar a **Multa por Estouro Horário** vinculada à categoria do apartamento.

### Cenário Prático com Aplicação de Multa Fracionada

Considerando a mesma jornada de 5 horas do exemplo anterior (1 período contratado de 3h + 2 horas de excesso), se o quarto possuir uma regra de multa de **R$ 5,00 a cada 30 minutos** de atraso:

1. **Custo do Período Base (Primeiras 3 horas):** R$ 9,00.
    
2. **Tempo Excedente:** 2 horas (120 minutos).
    
3. **Frações de Multa:** 120 minutos / 30 minutos = 4 períodos de multa.
    
4. **Custo da Multa:** 4 x R$ 5,00 = R$ 20,00.
    
5. **Valor Corrigido do Fechamento:** R$ 9,00 (base) + R$ 20,00 (multa) = **R$ 29,00**.
    

> [!tip] Flexibilidade de Configuração O administrador pode parametrizar o sistema para que, após um determinado limite de minutos de estouro, a penalidade mude automaticamente a cobrança para o valor de uma nova **Diária Completa**, inibindo a necessidade de cálculos manuais pelo recepcionista.

# Pontos Críticos e Roadmap do Módulo

> [!warning] Customização de Telas e Campos de Horário Para empresas que operam exclusivamente com diárias diurnas (pousadas/hotéis), campos de controle de minutos e horas poluem a interface. O sistema dispõe de um painel de **Personalização de Layout**, permitindo ocultar colunas de horários e ativar campos focados em `Status Atual` e contagem de dias, limpando a tela para o operador.

> [!danger] Integração de Consumo de Produtos (Gargalo de Lançamento) Lançar produtos consumidos pelos hóspedes (Frigobar/Restaurante) de forma isolada duplica o trabalho de fechamento no caixa do hotel.
> 
> - **Solução Arquitetural em Desenvolvimento:** O módulo de hotelaria receberá uma aba de **Consumos**, que estará vinculada por trás da interface ao módulo padrão de [[Vendas / Pedidos]]. Toda água, petisco ou item consumido será lançado como um produto dentro de um pedido oculto associado ao número do quarto. No momento do check-out, o sistema puxará o valor da hospedagem e somará os itens do pedido, gerando um único recebimento no [[PDV]] e facilitando a emissão da nota fiscal correspondente.
>