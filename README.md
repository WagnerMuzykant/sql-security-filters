

<img width="480" height="384" alt="the matrix GIF" src="https://github.com/user-attachments/assets/aaa8ff25-c34c-428e-98cf-49b5d141de0e" /><img width="480" height="384" alt="the matrix GIF" src="https://github.com/user-attachments/assets/aaa8ff25-c34c-428e-98cf-49b5d141de0e" />







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

### 3. Recuperar tentativas de login fora do México
Após o time determinar que a atividade suspeita não se originou no México, precisei filtrar as tentativas de login originadas no restante do mundo.

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```
<img width="672" height="145" alt="image" src="https://github.com/user-attachments/assets/5b8ed595-0797-4b39-99fd-b474cc37d229" />

> **Lógica aplicada:** Como os registros na coluna país podiam estar escritos como "MEX" ou "MEXICO", combinei o operador `NOT` com o operador `LIKE` e o caractere curinga `%`. O padrão `'MEX%'` engloba tudo que começa com essas letras, e o `NOT` exclui especificamente essas origens dos resultados.

### 4. Recuperar funcionários de Marketing no prédio leste
A equipe de segurança precisava atualizar máquinas em um local específico.

```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East-%';
```
<img width="670" height="193" alt="image" src="https://github.com/user-attachments/assets/45b7e193-207e-4178-9c91-61db328076b4" />

> **Lógica aplicada:** Utilizei o operador `AND` para exigir o cumprimento de duas regras: o funcionário deve pertencer ao departamento de 'Marketing', e estar alocado no prédio East. Como o prédio tem várias salas diferentes, utilizei o operador `LIKE` com o padrão `'East-%'` para capturar qualquer número de sala que venha após o prefixo.

### 5. Recuperar funcionários de Finanças ou Vendas
Para realizar a segunda fase das atualizações de segurança do sistema, precisei identificar as máquinas do pessoal de Vendas e Finanças.

```sql
SELECT *
FROM employees
WHERE department = 'Sales' OR department = 'Finance';
```
<img width="672" height="186" alt="image" src="https://github.com/user-attachments/assets/bbf8ea4e-3599-4630-bbf6-9a65796633dd" />

> **Lógica aplicada:** Usando o operador `OR` na mesma coluna de departamento, o banco de dados filtrou e me retornou uma lista consolidada contendo todos os funcionários que pertencem a uma equipe ou a outra.

### 6. Recuperar todos os funcionários que não são de TI
Para finalizar a rotina de atualizações, foi necessário identificar as máquinas de todos os outros departamentos da empresa, com exceção da equipe de TI, que já havia recebido o patch de segurança.

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```
<img width="671" height="173" alt="image" src="https://github.com/user-attachments/assets/d82cd89d-7430-491e-98c9-f4c1aee4ec87" />

> **Lógica aplicada:** Utilizei o operador `NOT` para negar a condição, excluindo especificamente o departamento 'Information Technology' dos resultados retornados pelo banco.

---

## 📝 Resumo e Aprendizados

A execução destas atividades consolida a capacidade de utilizar o SQL como uma ferramenta de resposta a incidentes. Através do cruzamento de cláusulas `WHERE` com operadores lógicos (`AND`, `OR`, `NOT`) e filtros de padrão (`LIKE`, `%`), é possível triar gigabytes de dados de logs em segundos, isolando ameaças ou definindo alvos para manutenção preventiva na infraestrutura corporativa.




