# 🛡️ Aplicação de Filtros em Consultas SQL para Cibersegurança

Neste projeto de laboratório prático, atuei no cenário de um profissional de segurança cibernética utilizando **SQL (Structured Query Language)** para investigar potenciais incidentes e realizar auditorias de equipamentos. 

O foco da atividade foi manipular, filtrar e analisar registros de bancos de dados corporativos (tabelas `employees` e `log_in_attempts`) para isolar eventos suspeitos utilizando operadores lógicos e caracteres curingas.

## 🎯 Descrição do Projeto

Como parte da equipe de segurança de uma grande organização, recebi duas missões principais:
1. Investigar tentativas de login incomuns (fora do horário comercial e em datas/locais suspeitos).
2. Identificar máquinas de funcionários específicos que necessitavam de atualizações críticas de segurança.

---

## 💻 Consultas SQL e Análise de Logs

Abaixo estão as consultas executadas durante a investigação, acompanhadas dos resultados e da lógica utilizada para a filtragem dos dados.

### 1. Recuperar tentativas de login com falha após o horário comercial
Para investigar um possível incidente de segurança ocorrido fora do expediente, a consulta filtra a tabela `log_in_attempts` para exibir apenas os logins malsucedidos ocorridos após as 18h. 

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00:00' AND success = 0;
```

<img width="672" height="146" alt="image" src="https://github.com/user-attachments/assets/d1530acc-ed45-44e8-835a-5f7a5b6600a0" />

> **Lógica aplicada:** Utilizei o operador lógico `AND` para garantir que o banco de dados retornasse apenas as linhas que atendessem simultaneamente a duas condições: a hora do login ser estritamente maior que 18:00:00, e o status de sucesso ser falso/zero (0).

### 2. Recuperar tentativas de login em datas específicas
Para investigar um evento suspeito ocorrido no dia 09/05/2022, precisei analisar todos os acessos daquele dia e do dia anterior.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

<img width="672" height="145" alt="image" src="https://github.com/user-attachments/assets/b45e5ff1-a8cb-4ec9-9d1d-ef26b4525928" />

> **Lógica aplicada:** A consulta utiliza o operador lógico `OR`. Isso instrui o SQL a retornar qualquer registro cuja data seja exatamente a primeira OU a segunda, permitindo cruzar os dados de ambos os dias na mesma saída.


