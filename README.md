# Teste de Performance – BlazeDemo

## 📌 Objetivo

Este projeto tem como objetivo validar a performance do fluxo de **compra de passagem aérea** da aplicação BlazeDemo, conforme o critério de aceitação definido no teste técnico.

URL testada: [https://www.blazedemo.com](https://www.blazedemo.com)

---

## 🎯 Critério de Aceitação

* Sustentar **250 requisições por segundo**
* **Percentil 90** do tempo de resposta **inferior a 2 segundos**

---

## 🛠️ Ferramentas Utilizadas

* **Apache JMeter 5.6.3**
* Sistema operacional: Windows
* Execução em modo **non-GUI** para maior fidelidade dos resultados

---

## 📁 Estrutura do Projeto

```
├── BlazeDemo teste requisicao.jmx
├── result.jtl
├── report/
│   └── index.html
└── README.md
```

---

## ▶️ Como Executar o Teste

### 1️⃣ Pré-requisitos

* Java 8 ou superior
* Apache JMeter 5.6.3 instalado

### 2️⃣ Execução em modo non-GUI

A partir do diretório `bin` do JMeter, execute o comando abaixo:

```powershell
.\jmeter -n -t "BlazeDemo teste requisicao.jmx" -l result.jtl -e -o report
```

Ao final da execução, será gerado um relatório HTML no diretório `report`.

### 3️⃣ Visualização do Relatório

Abra o arquivo abaixo em um navegador:

```
report/index.html
```

---

## ⚙️ Configuração do Teste

* **Usuários simultâneos:** 300
* **Ramp-up:** 60 segundos
* **Duração:** 10 minutos
* **Vazão controlada:** Constant Throughput Timer
* **Fluxo testado:**

  * Home
  * Buscar Voos
  * Escolher Voo
  * Confirmar Compra

---

## 📊 Resultados Obtidos

### Resumo Geral

* **Total de requisições:** 105.807
* **Throughput médio:** ~174 requisições por segundo
* **Taxa de erro:** 0,79%
* **Tempo médio de resposta:** ~1.051 ms

### Percentis de Tempo de Resposta (Total)

* **90th percentile:** 3.067 ms
* **95th percentile:** 4.015 ms
* **99th percentile:** 9.127 ms

---

## 🧠 Análise dos Resultados

O teste foi executado com o objetivo de validar o critério de aceitação de 250 requisições por segundo com o percentil 90 inferior a 2 segundos.

Durante a execução, observou-se que a aplicação atingiu um throughput médio de aproximadamente **174 requisições por segundo**. A partir desse ponto, houve **degradação progressiva dos tempos de resposta**, indicando saturação da aplicação.

O **percentil 90 apresentou valor médio de 3.067 ms**, ultrapassando o limite estabelecido de 2 segundos. Além disso, foram observados picos elevados no percentil 99, evidenciando impacto significativo sob carga elevada.

A taxa de erro permaneceu abaixo de 1%, indicando que a aplicação continuou respondendo às requisições, porém com aumento relevante de latência.

---

## ❌ Conclusão

O critério de aceitação **não foi atendido**, pois a aplicação não sustentou a vazão de **250 requisições por segundo** mantendo o **percentil 90 abaixo de 2 segundos**.

Os resultados indicam que o sistema apresenta limitações de escalabilidade quando submetido a cargas elevadas, comportamento esperado para uma aplicação de demonstração como o BlazeDemo.

---

## 📌 Considerações Finais

* O teste foi executado seguindo boas práticas de testes de performance
* A execução em modo non-GUI garante maior confiabilidade dos dados
* Os resultados refletem o comportamento real da aplicação sob carga

Este projeto demonstra a aplicação prática de testes de carga, análise de métricas e tomada de decisão baseada em dados.
