[[NOTA FISCAL]] e [[CASOS UP]]
INFORMOU QUE NAO ESTAVA CONSEGUINDO ALTERAR O VALOR DO PRODUTO NO PDV/TELA TOUCH:

SOLUÇÃO:
* o produto deve esta marcado para alterar preço e na tela de pedido de vendas, a box Alterar valor unitário do item na venda
-------------------------------------------------------------------------
Como  colocar acréscimo rateado no valor dos produtos na Nota Fiscal

SOLUÇÃO:
* Na configuração do pedido de venda, marcar a opção de desconto desejado
* ![[enviar desconto NF.png]]
-------------------------------------------------------------------------
Zerar Estoque de todos os produtos cadastrados no Sistema

SOLUÇÃO:
* Inventario estoque-> Incluir-> Status Digitando→Estoqiue → Acertar Estoque →Exportar Excel
- IMPORTANTE PASSAR O —— QUAL PREÇO——- PARA QUE SEJA PUXADO A INFORMAÇÃO CORRETA DOS VALORES DOS PRODUTOS
- EXPORTAR A GRADE DE PRODUTOS DENTRO DO CADASTRO DE PRODUTOS
![[ACERTO_INVENTARIO.png|697]]
* No arquivo Excel, de deixar apenas o campo ID e ESTOQUE ATUAL→ SALVAR E IMPORTAR NO RETAGUARDA
- Mudar o STATUS → ATIVO(para que seja realizado a mudança do estoque) → SALVAR