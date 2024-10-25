# Processo de ETL utilizando Power Query 🎯 


### Objetivo 🎯 

Esse projeto tem como objetivo praticar minhas habilidades de integração de banco de dados com Power BI e utlizar o Power Query para fazer um processo de ETL.
dos dados

### Descrição

Integrar uma base de dados do MySQL com o Power BI envolve a conexão do Power BI à sua base de dados MySQL e a importação dos dados para análise e visualização. Aqui estão os passos principais:

### 1. Instalar o Conector ODBC do MySQL

Baixe e instale o MySQL ODBC Driver. Esse driver permitirá que o Power BI se conecte ao MySQL.
Durante a instalação, siga as instruções para configurar a fonte de dados ODBC no seu sistema.

### 2. Configurar a Fonte de Dados ODBC

Abra o "Painel de Controle" no Windows e vá até "Ferramentas Administrativas" > "Fonte de Dados ODBC".
Na aba "DSN de Sistema", clique em "Adicionar" e selecione "MySQL ODBC Driver".
Preencha os detalhes da conexão, como Nome do servidor, Usuário, Senha, Nome da base de dados, e teste a conexão.

### 3. Conectar o Power BI ao MySQL

Abra o Power BI Desktop.
Clique em Obter Dados (Get Data) na aba "Página Inicial".
Na lista de fontes de dados, selecione Banco de Dados ODBC.
No campo de DSN, escolha o nome da fonte de dados que você configurou na etapa anterior.
Insira as credenciais (usuário e senha) quando solicitado.

###4. Importar e Modelar os Dados

No Power Bi vai em obter dados e escolha o banco ODBC e faça a conexão
Após a conexão, você verá uma lista de tabelas disponíveis no banco de dados.
Selecione as tabelas ou visualizações que você deseja carregar.

### Utilizando uma lista de passo faça o que pede a lista 

Passoa à passo

Para realizar essas tarefas no Power BI, você precisará fazer várias etapas, como verificação de tipos de dados, tratamento de valores nulos e ajustes de colunas complexas. Aqui está um guia detalhado para cada uma dessas atividades:

### 1. Verificação de Cabeçalhos e Tipos de Dados:

No Power Query Editor, selecione a tabela employee e verifique os tipos de dados de cada coluna.
A coluna Salary (Salário) deve ser ajustada para o tipo Decimal Number (Número Decimal) se ainda não estiver.
Clique com o botão direito na coluna Salary > Change Type > Decimal Number.
Faça o mesmo para outras colunas que representam valores numéricos ou monetários (como Hours na tabela works_on).

### 2. Modificar Valores Monetários para Tipo Double:

A coluna Salary que foi ajustada para Decimal Number já representa um tipo de dado double precision no Power BI.
Você pode repetir esse processo para outras colunas monetárias (caso existam) na sua base de dados.

### 3. Verificação de Nulos e Tratamento:

Na tabela employee, verifique se há valores nulos na coluna Super_ssn:
No Power Query Editor, filtre a coluna Super_ssn e escolha Null para ver os registros que possuem valores nulos.
Esses funcionários com Super_ssn nulo podem ser os gerentes, uma vez que não têm supervisores diretos. Certifique-se de que eles sejam realmente os gerentes.
Caso existam valores nulos em outras colunas (como em Salary ou Dno), você pode decidir preencher esses valores ou removê-los.
Para remover registros nulos, clique com o botão direito na coluna > Remove Empty (Remover Vazio).

### 4. Verificação de Colaboradores sem Gerente:

Para verificar se algum colaborador não possui gerente, filtre a coluna Super_ssn para Null:
Home > Transform Data > Filter Rows na coluna Super_ssn, e selecione valores nulos.
Se esses colaboradores são os gerentes (verificando pela função ou pela ausência de outros supervisores), eles podem ser mantidos como tal.

### 5. Verificação de Departamentos sem Gerente:

Na tabela departament, verifique se há algum valor nulo na coluna Mgr_ssn (que indica o gerente do departamento).
Aplique o filtro na coluna Mgr_ssn e veja se há departamentos com Null.
Se houver, e você tiver os dados do gerente, insira manualmente esses valores:
Clique com o botão direito na célula nula, escolha Replace Values (Substituir Valores) e insira o Ssn correto do gerente.

Preenchimento de Lacunas de Gerente:

Para preencher manualmente os dados de um gerente que estiver faltando:
No Power Query Editor, encontre a célula com Null na coluna Mgr_ssn da tabela departament.
Substitua o valor nulo pelo Ssn correto do funcionário que é o gerente daquele departamento.
Após corrigir, clique em Close & Apply para aplicar as mudanças.

### 7. Verificação de Horas Trabalhadas nos Projetos:

Na tabela works_on, verifique se há inconsistências nas horas trabalhadas (Hours). Para isso:
No Power Query Editor, selecione a coluna Hours e verifique os valores.
Você pode usar a funcionalidade Statistics para obter informações sobre os valores (média, mínimo, máximo, etc.).
Clique com o botão direito na coluna Hours > Statistics.

### 8. Separar Colunas Complexas:

Se houver colunas com dados complexos ou concatenados (por exemplo, endereços completos), você pode separá-las.
Selecione a coluna que deseja dividir (por exemplo, a coluna Address na tabela employee).
Use a funcionalidade Split Column (Dividir Coluna):
Clique com o botão direito na coluna Address > Split Column > Escolha dividir por delimitador (como hífen, se o endereço estiver formatado como "731-Fondren-Houston-TX").
Divida a coluna em componentes individuais, como Rua, Cidade, Estado.

### Para realizar a mesclagem das tabelas employee e departament no Power BI, você pode seguir os seguintes passos:

Etapas no Power BI:

### 1. Com as tabelas carregadas, vá até Home (Página Inicial) > Transform Data (Transformar Dados) para acessar o Power Query Editor.

Mesclando as Consultas:

No Editor de Consultas, selecione a tabela employee.
Clique em Home > Merge Queries (Mesclar Consultas) > Merge Queries as New (Mesclar Consultas como Novo).
Na janela de mesclagem, escolha a tabela departament como a segunda tabela para mesclagem.
Selecione a coluna Dno da tabela employee e a coluna Dnumber da tabela departament, já que estas colunas são as chaves estrangeiras que conectam as duas tabelas.
Defina o tipo de junção como Left Outer Join (Juncão Externa à Esquerda), pois queremos manter todos os registros da tabela employee e associar o nome do departamento correspondente.
Clique em OK.

Expandir a Tabela Mesclada:

Após a mesclagem, você verá uma nova coluna que contém uma tabela aninhada com os dados da departament.
Clique no ícone de expansão da coluna e selecione apenas a coluna Dname (Nome do Departamento) da tabela departament.
Renomeie a coluna para algo como "Department_Dname" (Nome do Departamento). O nome da tabela ficou como "colaborador/depart".

Aplicar as Alterações:

Após a mesclagem, clique em Close & Apply (Fechar e Aplicar) no Editor de Consultas para voltar à interface principal do Power BI.


### Para realizar a junção dos colaboradores com os nomes dos seus respectivos gerentes e mesclar as colunas de Nome (Fname) e Sobrenome (Lname) no Power BI, siga os passos detalhados abaixo:

Etapas no Power BI:

### Mesclagem das Tabelas para Relacionar Colaboradores com seus Gerentes:

Vá para Home (Página Inicial) > Transform Data (Transformar Dados) para acessar o Power Query Editor.
Mesclar a Tabela employee com Ela Mesma:

A lógica aqui é que você quer unir a tabela employee com ela mesma para trazer o nome dos gerentes (que também são funcionários). Siga os passos:
No Power Query Editor, selecione a tabela employee.
Clique em Home > Merge Queries (Mesclar Consultas) > Merge Queries as New (Mesclar Consultas como Novo).
Escolha a tabela employee novamente para mesclar com ela mesma.
Na tabela original (primeira), selecione a coluna Super_ssn e, na tabela mesclada (segunda), selecione a coluna Ssn. Isso criará uma relação entre os funcionários e seus gerentes.
Use um Left Outer Join (Juncão Externa à Esquerda) para garantir que todos os funcionários sejam mantidos, mesmo que não tenham um gerente.
Clique em OK.
Expandir a Tabela Mesclada:

Após a mesclagem, uma nova coluna será adicionada contendo as informações do gerente.
Clique no ícone de expansão da nova coluna, e selecione as colunas Fname e Lname (nome e sobrenome do gerente).
Renomeie essas colunas para algo como "Fname_gerentes" (Nome e sobrenome do Gerente) e "Fname_colaboradores" (Nome e sobrenome do colaborador). Depois em passos adiante vou renomear "Fname_colaboradores" por "numero_colaborador/gerente".

Vamos detalhar os passos para mesclar os nomes dos departamentos e suas localizações, agrupar os dados por gerente e eliminar as colunas desnecessárias no Power BI:

### 1. Mesclar Nomes de Departamentos e Localizações:
Você deseja que cada combinação de departamento e local seja única para auxiliar na criação de um modelo estrela. Aqui estão os passos:

Mesclagem das Colunas de Departamento e Localização:
No Power Query Editor, selecione a tabela dept_locations.
Selecione as colunas Dnumber (ou a coluna que contém o nome do departamento) e Dlocation.
Vá para Transform > Merge Columns (Mesclar Colunas).
Escolha um delimitador, como um hífen (-), para separar os valores.
Renomeei a nova coluna para algo como "department_location" (Departamento_Localização).
Agora, cada combinação de departamento e localização será tratada como um único valor, o que é útil para o modelo estrela.

### 2. Agrupar Dados por Gerente e Contar o Número de Colaboradores:

Agora você quer agrupar os dados para contar quantos colaboradores estão associados a cada gerente.

Agrupando Dados por Gerente:
Ainda no Power Query Editor, selecione a tabela employee.
Certifique-se de que a coluna com o nome do gerente já foi criada no passo anterior ("Manager Name").
Vá para Transform > Group By (Agrupar Por).
No diálogo de agrupamento, escolha agrupar pela coluna "Manager Name".
Na parte inferior, escolha Count Rows (Contar Linhas) como a operação de agregação. Isso contará quantos colaboradores estão associados a cada gerente.
Renomeei a coluna gerada para algo como "numero_colaborador/gerente" número_colaboradores/gerente).

### 3. Eliminação de Colunas Desnecessárias:

Para otimizar seu modelo e evitar o uso de dados desnecessários no relatório, você pode remover colunas que não serão usadas.

Eliminar Colunas Não Utilizadas:

Na tabela employee, verifique as colunas que não serão utilizadas, como Minit (nome do meio), Bdate (data de nascimento), Address, etc., dependendo do seu foco no relatório.

Clique com o botão direito na coluna > Remove (Remover).

Na tabela dept_locations, após mesclar os nomes de departamento e localização, você pode remover as colunas originais de Dnumber e Dlocation:

Selecione as colunas antigas e remova-as.
A mesma abordagem pode ser aplicada a outras tabelas, como departament, works_on e project, eliminando colunas que não fazem sentido para o seu relatório atual.

### 4. Aplicar as Alterações:
Quando tiver feito todas as modificações necessárias (mesclagens, agrupamentos e eliminação de colunas), clique em Close & Apply (Fechar e Aplicar) no Power Query Editor para voltar à interface principal do Power BI.


## 📚 Download

- [MySQL ODBC Driver](https://dev.mysql.com/downloads/connector/odbc/)

## 💻 Stacks utilizadas


<img src="https://upload.wikimedia.org/wikipedia/commons/c/cf/New_Power_BI_Logo.svg" alt="Power BI Logo" width="50"/>             <img src="https://upload.wikimedia.org/wikipedia/en/d/dd/MySQL_logo.svg" alt="MySQL Logo" width="100"/> <img src="https://upload.wikimedia.org/wikipedia/commons/8/87/Sql_data_base_with_logo.png" alt="SQL Logo" width="100"/>
