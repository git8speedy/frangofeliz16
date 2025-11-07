# Feature: Botão de Ação Rápida "Pagar/Receber"

## Data: 06/11/2025

### Implementação

Adicionado botão de ação rápida na página de Lançamentos Financeiros para facilitar a marcação de pagamentos/recebimentos.

### Funcionalidades Implementadas

#### 1. Botão de Ação Rápida na Lista
- ✅ Botão "Pagar" aparece para **despesas** com status **pendente**
- ✅ Botão "Receber" aparece para **receitas** com status **pendente**
- ✅ Botão só é exibido quando o status é "pendente"
- ✅ Ao clicar, atualiza automaticamente o status:
  - Despesas: `pendente` → `pago`
  - Receitas: `pendente` → `recebido`
- ✅ Ícone CheckCircle para indicar ação de confirmação
- ✅ Tooltip explicativo ao passar o mouse

#### 2. Status Inteligentes no Formulário
- ✅ **Para Despesas**: Mostra apenas "Pendente", "Pago" e "Cancelado"
- ✅ **Para Receitas**: Mostra apenas "Pendente", "Recebido" e "Cancelado"
- ✅ **Para Transferências**: Mostra "Pendente", "Pago", "Recebido" e "Cancelado"
- ✅ **Validação Automática**: Ao mudar o tipo de lançamento, o status é ajustado automaticamente:
  - Se mudar de Receita para Despesa e estava "recebido" → muda para "pendente"
  - Se mudar de Despesa para Receita e estava "pago" → muda para "pendente"

### Arquivo Modificado

**src/pages/Financas/Lancamentos.tsx**
- Importado ícone `CheckCircle` do lucide-react
- Adicionada função `handleQuickPay()` para atualização rápida de status
- Adicionado botão condicional na tabela de lançamentos
- Ajustado o select de status para filtrar opções por tipo
- Adicionada lógica para validar status ao mudar tipo de lançamento

### Exemplo de Uso

1. **Lista de Lançamentos:**
   ```
   Despesa de R$ 500,00 | Status: PENDENTE | [Pagar] [Editar] [Copiar] [Excluir]
   Receita de R$ 1000,00 | Status: PENDENTE | [Receber] [Editar] [Copiar] [Excluir]
   ```

2. **Ao Criar/Editar Despesa:**
   - Status disponíveis: Pendente, Pago, Cancelado
   
3. **Ao Criar/Editar Receita:**
   - Status disponíveis: Pendente, Recebido, Cancelado

### Benefícios

✅ **Usabilidade**: Ação rápida sem precisar abrir o formulário de edição
✅ **Intuitividade**: Nomenclatura correta (Pagar para despesas, Receber para receitas)
✅ **Validação**: Previne erros de status incompatíveis com o tipo de lançamento
✅ **Eficiência**: Reduz cliques necessários para marcar um pagamento
✅ **Visual Claro**: Botão destacado apenas para itens pendentes

### Fluxo de Trabalho Melhorado

**Antes:**
1. Clicar em "Editar"
2. Abrir formulário completo
3. Mudar status de "Pendente" para "Pago"/"Recebido"
4. Clicar em "Atualizar"
5. Fechar modal

**Depois:**
1. Clicar em "Pagar" ou "Receber" ✅ (1 clique!)

### Observações Técnicas

- O botão usa a mutation `updateTransaction` já existente
- A atualização é otimista e revalida os dados automaticamente
- O botão respeita o mesmo sistema de permissões das outras ações
- Compatível com o sistema de triggers do banco de dados para atualização de saldos
