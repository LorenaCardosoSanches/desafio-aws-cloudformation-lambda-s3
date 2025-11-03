# 💡 Insights e Aprendizados do Projeto

## 📘 Visão Geral

Este documento reúne as principais lições, reflexões e boas práticas aprendidas durante o desenvolvimento do **desafio final da formação AWS Cloud Foundations – DIO & Santander Code Girls**, que envolveu a criação de uma arquitetura automatizada utilizando **AWS CloudFormation**, **Amazon S3**, **AWS Lambda** e **CloudWatch Logs**.

O projeto consolidou a compreensão de conceitos essenciais de **Infraestrutura como Código (IaC)** e demonstrou o poder da **automação serverless** na nuvem AWS.

---

## 🧠 Principais Aprendizados

### **1️⃣ CloudFormation – Infraestrutura como Código (IaC)**

- Com o **CloudFormation**, aprendi a descrever uma infraestrutura completa em um arquivo YAML, de forma declarativa e reprodutível.  
- O uso de templates permite criar e destruir ambientes inteiros com apenas alguns cliques.  
- Essa abordagem garante **consistência**, **agilidade** e **padronização** entre diferentes ambientes (dev, teste e produção).  
- Também compreendi a importância de **dependências explícitas** (`DependsOn`) para evitar erros de referência e garantir a ordem correta na criação dos recursos.  

> ✨ *Lição prática:* um template bem estruturado é o coração de uma boa automação na AWS.

---

### **2️⃣ Lambda e S3 – Automação Serverless**

- A integração entre **Amazon S3** e **AWS Lambda** representa o verdadeiro conceito de **automação em nuvem**: um serviço reage automaticamente às ações de outro.  
- Ao enviar um arquivo ao bucket S3, o evento `s3:ObjectCreated` dispara a função Lambda, que processa o evento sem a necessidade de manter servidores.  
- Essa abordagem é **escalável**, **eficiente** e **custo-efetiva**, ideal para pipelines de dados, validação de arquivos e processamento sob demanda.  
- Entendi também a importância da **IAM Role** e da permissão `AWS::Lambda::Permission` para garantir que a comunicação entre serviços seja segura e controlada.  

> ✨ *Lição prática:* pequenas automações serverless podem substituir infraestruturas complexas com muito menos custo e manutenção.

---

### **3️⃣ CloudWatch Logs – Monitoramento e Observabilidade**

- O **Amazon CloudWatch Logs** foi essencial para acompanhar o comportamento da função Lambda e validar se o fluxo estava funcionando corretamente.  
- Aprendi a interpretar logs, identificar eventos de sucesso e falha, e utilizar as informações de execução para melhorar o código.  
- Esse monitoramento contínuo reforça a importância da **observabilidade** em ambientes cloud.

> ✨ *Lição prática:* a automação só é completa quando é também observável e auditável.

---

## ⚙️ Boas Práticas Aplicadas

- Organização e **versionamento do código** com GitHub.  
- Uso de **nomes claros e descritivos** para stacks e recursos.  
- Implementação de **arquitetura mínima funcional**, evitando complexidade desnecessária.  
- **Validação do template** antes do deploy (`aws cloudformation validate-template`).  
- Criação de **documentação completa** e evidências (prints, diagrama e README detalhado).  

---

## 🌐 Reflexão sobre o Aprendizado

Durante o desafio, ficou evidente que **a automação não é apenas sobre tecnologia**, mas sobre **processo e confiabilidade**.  
Ao utilizar o CloudFormation para definir toda a infraestrutura e o Lambda para automatizar tarefas, o aprendizado se estendeu para além da técnica — foi um exercício de **planejamento, documentação e boas práticas de DevOps**.

> 🧩 *Com o domínio dessas ferramentas, é possível construir soluções escaláveis, seguras e automatizadas, reduzindo esforço operacional e aumentando a eficiência.*

---

## 🧾 Conclusão

Este projeto foi uma oportunidade prática de unir teoria e execução em um ambiente real da AWS.  
A experiência demonstrou como **CloudFormation**, **S3**, **Lambda** e **CloudWatch Logs** se complementam para criar fluxos automatizados, seguros e de fácil manutenção.

A integração entre esses serviços exemplifica o poder do **modelo serverless** e a importância da **Infraestrutura como Código (IaC)** no desenvolvimento moderno em nuvem.

---

📝 **Anotação criada por:** Lorena Cardoso Sanches  
🎓 **Formação:** AWS Cloud Foundations – DIO & Santander Code Girls  
📅 **Ano:** 2025
