## DIO - Bootcamp GFT - Fundamentos de Cloud com AWS

<br>

##  🚀 Desafio - Implementar Infraestrutura Automatizada com AWS CloudFormation

# 🤖 Automação de Infraestrutura Global com AWS CloudFormation

Este repositório foi desenvolvido como o entregável prático para o desafio de **Automação de Infraestrutura**. O objetivo principal é documentar a transição do gerenciamento manual de TI para a cultura de **Infraestrutura como Código (IaC)**, utilizando o AWS CloudFormation.

---

## 🎯 Objetivos do Projeto

*   **Eliminar o Trabalho Manual (ClickOps):** Substituir a criação de recursos pelo painel visual por scripts automatizados e repetíveis.
*   **Padronização de Ambientes:** Garantir que as configurações de segurança (como criptografia e versionamento) sejam aplicadas automaticamente em qualquer nova implantação.
*   **Documentação Viva:** Utilizar este repositório como um guia técnico de consulta rápida para futuras implementações em cenários reais.

---

## 💾 Código da Infraestrutura Automatizada (template.yaml)

O script abaixo automatiza a criação de um **Bucket Amazon S3 seguro** e de uma **Fila de Mensageria Amazon SQS**. Este código foi testado e estruturado para garantir isolamento total e conformidade com as regras de nomenclatura da AWS.

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'Infraestrutura Automatizada - Bucket S3 Seguro e Fila SQS para E-Commerce.'

Resources:
  # Automação do Armazenamento Seguro
  BucketArmazenamentoEstudos:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: !Sub 'provedor-automatizado-s3-\${AWS::AccountId}'
      VersioningConfiguration:
        Status: Enabled
      BucketEncryption:
        ServerSideEncryptionConfiguration:
          - ServerSideEncryptionByDefault:
              SSEAlgorithm: AES256

  # Automação da Fila de Mensageria
  FilaPedidosAutomatizada:
    Type: 'AWS::SQS::Queue'
    Properties:
      QueueName: 'FilaProcessamentoPedidos'
      VisibilityTimeout: 30
```

---

## 🧠 Insights e Aprendizados Práticos sobre Automação

### 1. O Conceito de Repetibilidade Segura (Idempotência)
A automação com CloudFormation garante a consistência do ambiente. Se este template for executado por 10 analistas diferentes, em 10 contas AWS distintas, o resultado final será rigorosamente idêntico. O motor do CloudFormation analisa o estado atual da conta e apenas cria o que falta, sem gerar duplicidades ou conflitos de recursos.

### 2. Tratamento Automático de Falhas (Rollback Atômico)
Um dos maiores aprendizados sobre automação em nuvem é o comportamento atômico da Stack. Se o CloudFormation estiver criando 5 recursos e o último falhar por falta de permissão, a automação entra em estado de `ROLLBACK_IN_PROGRESS` e **desfaz tudo automaticamente**, limpando o ambiente. Isso evita o cenário de "recursos fantasmas" órfãos gerando cobranças desconhecidas na conta.

---

## 🛠️ Paralelo de Carreira: Da Malha de Produção à Nuvem Automatizada

Para profissionais com bagagem em ambientes tradicionais padronizados, como as arquiteturas de **Mainframe**, o CloudFormation guarda uma semelhança conceitual profunda com a automação de rotinas via **JCL e utilitários de sistema**. 

No ambiente tradicional, a estabilidade depende de scripts perfeitamente parametrizados para alocar arquivos, volumes e gerenciar os códigos de retorno dos *Steps*. Na nuvem, o arquivo YAML do CloudFormation executa o exato mesmo papel de governança: ele dita as regras de alocação de recursos elásticos. 

A transição de ambiente não invalida essa experiência de controle estrito de processos; pelo contrário, a mentalidade de "produção limpa" e aversão ao erro manual típica de quem operou grandes sistemas é justamente o que o mercado de computação em nuvem busca ao implementar práticas de IaC de alto nível.

---

### <img width="20" height="20" alt="image" src="https://github.com/user-attachments/assets/3f883ffa-dbfb-43d7-ae40-bd9456d6440f" /> Agradecimentos

[Equipe GFT](https://www.gft.com/br/pt)

[Equipe DIO](https://www.dio.me)

Utilização de IA principalmente para tornar a documentação mais clara, objetiva e fluída.

Brasil, Julho de 2026
