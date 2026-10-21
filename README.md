# SmartFood — Análise e Redução do Desperdício Alimentar

## Descrição
Projeto ETL desenvolvido para analisar dados de consumo e desperdício alimentar em restaurantes/cantinas e calcular recomendações de preparação de pratos.

## Tecnologias
- Pentaho Data Integration (Kettle/Spoon) 9.4
- SQLite
- CSV e JSON
- SMTP/Gmail
- Dados sintéticos gerados para o projeto

## Dados
- 3 restaurantes
- 24 pratos
- 60 dias
- 1.440 registos de consumo

Fontes:
- `restaurantes.csv`
- `pratos.json`
- `consumos.csv`

## Processo ETL

### E — Extração
Leitura de dados provenientes de CSV e JSON.

### T — Transformação
- Junção de dados
- Ordenação e seleção de campos
- Cálculo do desperdício
- Cálculo da percentagem de desperdício
- Cálculo do custo do desperdício
- Agregação por restaurante e prato
- Cálculo de médias
- Cálculo da margem de desperdício
- Cálculo da preparação recomendada

### L — Load
Persistência dos resultados em SQLite e exportação das recomendações para:

`recomendacoes_finais.csv`

## Job

O processo completo é automatizado através de:

```text
Start → SQL → E_restaurantes → T_restaurantes → L_restaurantes → Email_restaurantes
```

A etapa SQL limpa os dados agregados anteriores antes de executar novamente o processo.

No final, as recomendações são enviadas automaticamente por email.

## Email
O email apresenta as recomendações de preparação para os três restaurantes, incluindo o prato e a quantidade recomendada.

## Resultados
O processo consegue:
- Processar 1.440 registos
- Analisar 24 pratos
- Analisar 3 restaurantes
- Calcular recomendações de preparação
- Guardar resultados em SQLite
- Exportar um CSV final
- Enviar automaticamente as recomendações por email

## Estrutura sugerida

```text
SmartFood/
├── dados/
│   ├── restaurantes.csv
│   ├── pratos.json
│   └── consumos.csv
├── pentaho/
│   ├── E_restaurantes.ktr
│   ├── T_restaurantes.ktr
│   ├── L_restaurantes.ktr
│   ├── Email_restaurantes.ktr
│   └── SmartFood.kjb
├── output/
│   └── recomendacoes_finais.csv
├── README.md
└── relatorio/
```

## Execução
1. Abrir o Pentaho Data Integration (Spoon).
2. Configurar a ligação SQLite.
3. Abrir o Job principal.
4. Executar o Job.
5. Verificar o CSV final e o email recebido.

## Objetivo
Demonstrar como um processo ETL pode transformar dados de consumo em informação útil para apoiar decisões de preparação de alimentos e contribuir para a redução do desperdício alimentar.

## Link de Video
https://youtu.be/_848QVEg7CQ
