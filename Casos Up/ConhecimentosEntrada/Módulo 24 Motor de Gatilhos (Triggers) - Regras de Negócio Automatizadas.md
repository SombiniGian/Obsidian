O "Motor de Gatilhos" é uma ferramenta avançada de automação que permite ao usuário criar regras de negócio personalizadas, sem a necessidade de solicitar alterações no código-fonte do ERP. Ele atua como um mecanismo de validação em tempo real, executando ações automáticas em resposta a eventos específicos (triggers) dentro das telas do sistema.

## 1. Conceito e Funcionamento Técnico

O gatilho funciona através da execução de comandos **SQL (Firebird)** no momento em que uma ação ocorre em uma tela (ex: Salvar, Incluir, Excluir).

* **Momento do Disparo:** O sistema monitora o ciclo de vida da transação. Quando o operador executa uma ação (clica em "Salvar", por exemplo), o motor de gatilhos intercepta essa ação antes que o _commit_ (gravação definitiva no banco) seja concluído.
* **Validação SQL:** O usuário deve escrever um comando `SELECT` que retorne um valor específico no campo `retorno`.
    * **Se o SQL retornar `NULL`:** O sistema entende que a regra foi cumprida e autoriza a operação.
    * **Se o SQL retornar qualquer valor:** O sistema dispara o gatilho, exibindo a mensagem configurada e executando a ação escolhida.
* **Visibilidade de Transação:** Uma vantagem técnica crucial é que o gatilho enxerga os dados que estão na "memória" da transação atual, mesmo que o registro ainda não tenha sido gravado no banco de dados. Isso permite validar dados recém-digitados pelo operador antes que eles se tornem permanentes.

---

## 2. Ações Possíveis após o Disparo

Quando uma condição configurada no gatilho é atendida, o sistema pode realizar três tipos de ações:

1. **Aviso Simples:** Exibe uma mensagem na tela para o usuário (informativa ou de alerta).
2. **Bloqueio Total:** Impede a conclusão da operação (ex: "Não é possível salvar este cliente sem grupo"). O botão de salvar torna-se inoperante até que a regra seja atendida.
3. **Senha de Liberação:** Permite que a operação continue apenas mediante a digitação de uma senha de liberação por um usuário com privilégios superiores. Esta ação é auditada automaticamente no log do sistema, registrando quem liberou, quando e qual foi a senha utilizada.

---

## 3. Exemplos Práticos de Aplicação

A "imaginação é o limite" para a criação de regras. Exemplos citados:

* **Validações de Campo Obrigatório:** Exigir que um campo específico (ex: "Placa do Carro" em uma OS) seja preenchido com um número mínimo de caracteres.
* **Regras de Venda e Preço:**
    * Bloquear a venda de produtos de um grupo específico para pagamentos "a prazo".
    * Impedir que o preço de venda de um produto seja inferior a um percentual sobre o valor de custo.
* **Integridade de Pedidos:** Obrigar que um pedido contenha um número mínimo de itens antes de ser finalizado.
* **Uso com ChatGPT:** Uma estratégia eficiente recomendada é utilizar IAs como o ChatGPT para estruturar a consulta SQL necessária. O usuário descreve a regra em linguagem natural ("Quero retornar o ID do cliente se o grupo estiver vazio no Firebird"), e a IA gera o código compatível, que é então colado no campo de comando SQL do gatilho.

---

## 4. Auditoria e Segurança

Toda vez que um gatilho é executado (especialmente quando exige senha), o sistema registra o evento na auditoria oficial. Isso garante que o gestor saiba exatamente quais regras foram violadas e, no caso de liberação, qual usuário autorizou a exceção, mantendo o controle total sobre a operação.