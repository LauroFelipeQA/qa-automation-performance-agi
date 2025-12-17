# Teste de Performance – BlazeDemo #
## 1. Objetivo ##

Este projeto tem como objetivo avaliar o desempenho da aplicação BlazeDemo no fluxo completo de compra de passagem aérea, utilizando o Apache JMeter 5.6.2 com Concurrency Thread Group, contemplando cenários de teste de carga e teste de pico.

## 2. Escopo do Teste ##

### Fluxo testado ###

Compra de passagem aérea com sucesso, incluindo:

- Acesso à página inicial
- Busca de voos
- Seleção de voo
- Confirmação da compra
- Critérios de aceitação

Carga:

- Throughput mínimo de 250 requisições por segundo
- 90º percentil < 2 segundos

Pico:

- Avaliar comportamento do sistema sob aumento abrupto de concorrência (sem SLA de tempo de resposta)

## 3. Ferramentas e Tecnologias ##

- Apache JMeter 5.6.2
- Plugin Concurrency Thread Group
- Execução em modo não-GUI
- Relatórios HTML nativos do JMeter

## 4. Estratégia de Teste ##

Os cenários de carga e pico foram executados de forma independente, conforme boas práticas de testes de performance, garantindo isolamento das métricas e melhor análise dos resultados.

## 5. Configuração dos Cenários ##
### 5.1 Teste de Carga ###

Parâmetro	Valor
Tipo de teste	Carga
- Concorrência alvo	250 usuários
- Ramp-up	2 minutos
- Tempo em carga	10 minutos
- Thread Group	Concurrency Thread Group

### 5.2 Teste de Pico ###
Parâmetro	Valor
Tipo de teste	Pico
- Concorrência alvo	500 usuários
- Ramp-up	1 minuto
- Tempo em pico	3 minutos
- Thread Group	Concurrency Thread Group

## 6. Execução dos Testes ##

Os testes foram executados em modo não-GUI, conforme comandos abaixo:

Teste de Carga
".\jmeter -n -t blazedemo_performance.jmx -l carga.jtl -e -o relatorio_carga"

Teste de Pico
".\jmeter -n -t blazedemo_performance.jmx -l pico.jtl -e -o relatorio_pico"

## 7. Resultados Obtidos ##
### 7.1 Teste de Carga ###

Métrica	Resultado
  Throughput	312,69 req/s
  90º Percentil	1433 ms
  Erros	0%

#### Análise: ####
O cenário de carga atendeu plenamente aos critérios de aceitação, superando a vazão mínima exigida e mantendo o tempo de resposta do 90º percentil abaixo de 2 segundos.

### 7.2 Teste de Pico ###
Métrica	Resultado
  Throughput	94,52 req/s
  90º Percentil	21.519 ms
  Erros	0%

#### Análise: ####
Durante o teste de pico, observou-se degradação significativa no tempo de resposta, comportamento esperado em cenários de estresse. Apesar da redução de throughput, a aplicação manteve estabilidade funcional, sem ocorrência de erros.

## 8. Conclusão ##

Os testes demonstraram que a aplicação suporta a carga esperada, atendendo aos requisitos de desempenho definidos, e apresenta comportamento previsível sob pico de acesso, com degradação controlada e sem falhas funcionais.

## 9. Observações Técnicas ##

O uso do Concurrency Thread Group permitiu maior controle sobre a concorrência e estabilidade da vazão.

Os testes de carga e pico foram executados separadamente para garantir clareza na análise dos resultados.

O teste de pico não possui SLA de tempo de resposta, sendo utilizado apenas para avaliação de resiliência.
