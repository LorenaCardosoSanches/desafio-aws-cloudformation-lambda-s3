# λ AWS Lambda e Amazon S3 – Integração e Funcionamento

## 📘 Visão Geral

O **AWS Lambda** é um serviço **serverless** que executa código automaticamente em resposta a eventos, sem necessidade de servidores dedicados.  
No projeto, ele foi integrado ao **Amazon S3**, que atua como **gatilho (trigger)**: toda vez que um novo objeto é criado no bucket, a função Lambda é acionada para processar esse evento.

Essa integração permite automatizar fluxos de trabalho como **processamento de arquivos**, **análises de logs** e **movimentação de dados**, sem infraestrutura física.

---

## 🧩 Conceitos-Chave

### **1️⃣ Amazon S3 (Trigger de evento)**
O **Amazon Simple Storage Service (S3)** é um serviço de armazenamento de objetos altamente escalável.  
No contexto do projeto, ele foi configurado para gerar eventos do tipo **`s3:ObjectCreated`**.

**Função no fluxo:**
- Recebe uploads de arquivos enviados pelo usuário.
- Dispara automaticamente um evento quando um novo arquivo é criado.
- Esse evento é encaminhado para a função Lambda configurada no CloudFormation.

**Exemplo do template:**
```yaml
NotificationConfiguration:
  LambdaConfigurations:
    - Event: "s3:ObjectCreated:*"
      Function: !GetAtt ProcessFunction.Arn
```

### **2️⃣ AWS Lambda (Processamento automático)**
O **AWS Lambda** é responsável por executar o código de forma automatizada sempre que ocorre o evento configurado no S3.
A função é criada diretamente no template.yaml, com o código embutido (inline code).

**Trecho do projeto:**
```yaml
Code:
  ZipFile: |
    import json
    def handler(event, context):
        print("Evento S3 recebido:", json.dumps(event))
        return {"status": "ok"}
```

O que acontece na prática:

1. O evento do **S3** é recebido pela **Lambda**.  
2. O código lê as informações do evento (bucket, chave do arquivo, etc.).  
3. O log de execução é enviado automaticamente ao **Amazon CloudWatch Logs**.

---

### 3️⃣ Permissão de Invocação (`LambdaInvokePermission`)

Para que o **S3** possa acionar a função **Lambda**, é necessário criar uma **permissão explícita** no **CloudFormation**.  
Sem essa permissão, a trigger não funcionaria corretamente.
No projeto, o SourceArn foi removido para evitar dependência circular entre o S3 e a Lambda.

**Trecho do template:**
```yaml
Type: AWS::Lambda::Permission
Properties:
  Action: lambda:InvokeFunction
  FunctionName: !Ref MinhaFuncaoLambda
  Principal: s3.amazonaws.com
  SourceArn: !GetAtt MeuBucketS3.Arn
```

Função dessa permissão:
Ela autoriza o serviço S3 a invocar a função Lambda quando um evento de criação de objeto ocorrer.

### 4️⃣ CloudWatch Logs (Monitoramento)

O **Amazon CloudWatch Logs** coleta automaticamente as saídas geradas pela **função Lambda**.  
Isso permite visualizar:

- Mensagens de sucesso ou erro  
- Estrutura do evento recebido  
- Tempo de execução e logs de *debug*

---

**Como acessar:**  
`AWS Console → CloudWatch → Logs → /aws/lambda/ProcessFunction`

## 🔍 Fluxo de Execução no Projeto

1️⃣ O usuário faz **upload** de um arquivo para o **bucket S3 (Input)**.  
2️⃣ O **S3** detecta o novo objeto e dispara o evento `s3:ObjectCreated`.  
3️⃣ O **AWS Lambda (ProcessFunction)** é acionado automaticamente.  
4️⃣ O código da **Lambda** processa o evento e imprime o log no console.  
5️⃣ O **CloudWatch Logs** armazena as mensagens e detalhes da execução.

---

## 💡 Boas Práticas

- Configurar eventos específicos no S3 (ex: apenas `s3:ObjectCreated`), evitando *triggers* desnecessárias.  
- Adicionar tratamento de exceções no código da Lambda (`try/except`).  
- Manter logs claros e informativos para facilitar o monitoramento.  
- Usar **variáveis de ambiente** na Lambda para definir buckets de saída ou parâmetros dinâmicos.  
- Limitar permissões no **IAM**, seguindo o princípio do **menor privilégio**.

---

## ✅ Conclusão

A integração entre **Amazon S3** e **AWS Lambda** é um exemplo prático de **automação serverless**, eliminando a necessidade de infraestrutura manual.  
No projeto, essa abordagem demonstrou a capacidade da **AWS** em executar funções sob demanda, processar eventos em tempo real e registrar logs automaticamente no **CloudWatch**, tudo orquestrado por um único *template* **CloudFormation**.

---

📝 **Anotação criada por:** Lorena Cardoso Sanches  
🎓 **Formação:** AWS Cloud Foundations – DIO & Santander Code Girls  
📅 **Ano:** 2025
