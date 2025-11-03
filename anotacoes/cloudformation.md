# ☁️ AWS CloudFormation – Anotações Técnicas

## 📘 Visão Geral

O **AWS CloudFormation** é um serviço que permite **criar, atualizar e excluir recursos da AWS de forma automatizada**, utilizando **Infraestrutura como Código (IaC)**.  
Em vez de configurar manualmente cada serviço no console, o CloudFormation permite descrever toda a infraestrutura em **arquivos YAML ou JSON**, chamados de *templates*.

---

## 🧩 Conceitos-Chave

### **1️⃣ Stack**
Uma *stack* é o conjunto de recursos definidos em um template CloudFormation.  
Cada stack representa uma infraestrutura completa — por exemplo, pode incluir buckets S3, funções Lambda e permissões IAM.

**Exemplo:**  
A stack `desafio-final-dio` cria automaticamente:
- Um **bucket S3** (armazenamento de arquivos)
- Uma **função Lambda** (automação)
- Uma **IAM Role** (permissões seguras)
- Um **CloudWatch Log Group** (monitoramento)

---

### **2️⃣ Template**
É o **arquivo declarativo** que descreve os recursos que serão criados.  
Ele define parâmetros, recursos, permissões e dependências entre serviços.

**Principais seções de um template YAML:**

| Seção | Descrição |
|-------|------------|
| `AWSTemplateFormatVersion` | Versão do formato do arquivo. |
| `Description` | Texto explicativo sobre o template. |
| `Parameters` | Valores variáveis que podem ser passados na criação da stack. |
| `Resources` | Lista dos recursos AWS a serem criados. |
| `Outputs` | Informações exibidas após a criação da stack (ex: nomes dos buckets). |

---

### **3️⃣ Recursos (Resources)**
Cada recurso é identificado por um nome lógico e um tipo.  
Os tipos seguem o formato:  
`AWS::<Serviço>::<Recurso>`

**Exemplo prático do projeto:**

```yaml
Resources:
  InputBucket:
    Type: AWS::S3::Bucket

  ProcessFunction:
    Type: AWS::Lambda::Function
```
Esses dois blocos criam um bucket S3 e uma função Lambda automaticamente.

### **3️⃣ Dependências**
Para garantir que os recursos sejam criados na ordem correta, é possível usar DependsOn.
No projeto, o S3 depende da permissão da Lambda (LambdaInvokePermission).

```yaml
DependsOn: LambdaInvokePermission
```
Isso evita erros de referência durante a execução da stack.

## 🧮 Vantagens do CloudFormation

- **Automação completa** da criação de infraestrutura.  
- **Padronização** entre ambientes (dev, teste e produção).  
- **Reprodutibilidade** — o mesmo template pode ser usado várias vezes.  
- **Controle de versão** via GitHub.  
- **Integração com outros serviços AWS** (como IAM, Lambda, S3 e CloudWatch).  

---

## 🔍 Fluxo de Execução

1️⃣ **Criação do template** `template.yaml` com os recursos necessários.  
2️⃣ **Upload do template** no console do **AWS CloudFormation**.  
3️⃣ **Definição do nome da stack** (ex: `desafio-final-dio`).  
4️⃣ O **CloudFormation** cria todos os recursos automaticamente.  
5️⃣ **Logs e status** são exibidos até que a stack atinja o estado **CREATE_COMPLETE**.  
6️⃣ Todos os recursos podem ser **excluídos com um único clique** em **Delete Stack**.  

---

## 💡 Boas Práticas

- Sempre adicionar **descrições claras** nos recursos.  
- Utilizar **nomes significativos** (ex: `InputBucket`, `ProcessFunction`).  
- Manter o template **organizado e comentado**.  
- Usar **controle de versão** no GitHub.  
- Validar o template com o comando:

```bash
aws cloudformation validate-template --template-body file://template.yaml
```
