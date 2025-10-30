# AWS-Laboratorio
Esse repositório é uma breve descrição sobre os principais ensinamentos no curso da AWS Cloud Foundations sobre AWS Step Functions Tutorial.


## 🧩 O que é o AWS Step Functions

O **AWS Step Functions** permite criar **máquinas de estados** (state machines) para controlar a execução de processos compostos por várias etapas, chamadas de **estados** (*states*).  
Esses estados podem executar funções Lambda, tomar decisões condicionais, aguardar eventos, rodar tarefas em paralelo e muito mais — tudo de forma escalável, tolerante a falhas e sem a necessidade de servidores.

---

## ⚙️ Conceitos Principais

| Conceito | Descrição |
|-----------|------------|
| **State Machine** | É o fluxo completo do processo (workflow). Cada etapa é um *estado*. |
| **State (Estado)** | Representa uma etapa do processo — pode ser tarefa, decisão, espera, etc. |
| **Task State** | Executa uma ação (como chamar uma função AWS Lambda). |
| **Choice State** | Permite definir condições (como “if/else”) para decidir o próximo passo. |
| **Parallel State** | Executa múltiplas tarefas simultaneamente. |
| **Wait State** | Adiciona um tempo de espera antes da próxima etapa. |
| **Pass State** | Apenas passa dados adiante sem executar ações (útil para testes). |
| **Fail / Succeed State** | Define o final do fluxo com falha ou sucesso. |
| **Execution** | Uma execução individual de uma máquina de estados. |
| **ASL (Amazon States Language)** | Linguagem JSON usada para definir as máquinas de estados. |

---

## 💡 Benefícios

✅ **Totalmente gerenciado:** sem necessidade de provisionar servidores.  
✅ **Visual e intuitivo:** criação de fluxos pelo console AWS.  
✅ **Escalável:** executa milhares de fluxos em paralelo.  
✅ **Tolerante a falhas:** reexecuta automaticamente em caso de erro.  
✅ **Integrado:** funciona com Lambda, ECS, SQS, SNS, Glue, DynamoDB, entre outros.  
✅ **Monitoramento:** logs detalhados via CloudWatch.

---

## 🧠 Casos de Uso

- Processamento de dados (ETL)
- Automação de tarefas de backend
- Orquestração de funções Lambda
- Processos de aprovação (ex: RH, finanças)
- Pipelines de Machine Learning
- Processos assíncronos complexos

---

## 🧱 Exemplo 1 — Fluxo Simples com AWS Lambda

Arquivo: `examples/simple-lambda-state-machine.json`

```json
{
  "Comment": "Exemplo simples de Step Function com Lambda",
  "StartAt": "ExecutarLambda",
  "States": {
    "ExecutarLambda": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGIAO:ID-CONTA:function:minhaFuncaoLambda",
      "Next": "Finalizar"
    },
    "Finalizar": {
      "Type": "Succeed"
    }
  }
}
