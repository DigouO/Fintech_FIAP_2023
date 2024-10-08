<div id="fase06" align="center">
<h1>FASE 6 - MODEL</h1>
<h2>Capítulo 08: Quando o café javanês consulta o oráculo.</h2>
</div>

<div align="center">
<h2>1. QUANDO O CAFÉ JAVANÊS CONSULTA O ORÁCULO</h2>
</div>

## 1.1 Introdução

- neste capítulo vamos ver o que o sistema deve fazer para interagir com os dados em um banco de dados.
- quais são os procedimentos necessários para que o sistema faça uso desse recurso tão essencial?

## 1.2 Recapitulando banco de dados

- a maioria dos sistemas precisa armazenar dados e informações para serem recuperados posteriormente. 

### a) `Sistemas de Gerenciamento de Banco de Dados` (SGBD):
- são sistemas especializados no armazenamento de dados, que oferecem funcionalidades e recursos avançados, como backup e pesquisas eficientes.
- SGBD é um conjunto de programas de computador responsáveis pelo gerenciamento de uma base de dados. 
- seu principal objetivo é retirar da aplicação cliente a responsabilidade de gerenciar acesso, manipulação e a organização dos dados. 
- o SGBD disponibiliza uma interface para que seus clientes possam realizar as operações de inclusão, alteração, exclusão e consulta de dados.
- os principais SGBDs utilizados aplicam o Modelo Relacional para armazenar informações e a linguagem (Structure Query Language) é utilizada para realizar as operações na base de dados. 
- principais SGBDs utilizados no mercado: Oracle Database, Microsoft SQL Server, PostgreSQL, Sysbase, MySQL Server, Apache Derby.

### b) `Modelo Relacional`:
- é um modelo de dados baseado em entidades e relacionamentos.
  - uma tabela armazena as informações relevantes da entidade.
  - a atribuição de valores de uma entidade constrói um registro da tabela.
  - a relação determina como cada registro da tabela se associa a registros de outras tabelas.
  - uma tabela é formada por registros (linhas) e os registros são formados por campos (colunas).
  - tabelas normalmente têm uma chave primária, que é um identificador único que garante que nenhum registro será duplicado. 

### c) SQL (Structured Query Language) ou Linguagem de Consulta Estruturada:
- é uma linguagem de pesquisa declarativa padrão para banco de dados relacional.
- por meio dela, os principais SGBDs interagem com os bancos de dados.
- alguns dos principais comandos SQL para manipulação de dados são: INSERT (inserção), UPDATE (atualização), SELECT (consulta) e DELETE(exclusão). 
- possibilita também criar tabelas, relações, controle de acesso, etc.

> Sistemas desenvolvidos na plataforma Java comunicam-se com o SGBD e manipulam seus dados utilizando a API Java DataBase Connectivity (JDBC)!

## 1.3 Java Database Connectivity

- é uma API (Application Programming Interface).
- contém um conjunto de regras que permite uma padronização no acesso aos diversos SGDBs disponíveis no mercado.
- define um conjunto de interfaces que devem ser implementadas pelas empresas fornecedoras de SGDB que desejam ser compatíveis com a plataforma Java.

> São os SGDBs que se adaptam à plataforma Java, por meio da implementação de um JDBC, e não o contrário! Todo o código implementado para sistema será o mesmo, pois as bibliotecas de acesso aos bancos de dados seguem os mesmos padrões.

- as bibliotecas de classes que permitem a integração de um SGDB à aplicação Java são chamadas `driver`.
- geralmente, as empresas fornecedoras de SGDBs oferecem o driver de conexão que seguem as especificações JDBC.

<div align="center">
<img src="./assets/estrutura-jdbc.png" width="50%">
<p><em>Estrutura JDBC.</em></p><br>
</div>

- uma das poucas classes que é implementada é a `DriverManager`, responsável por identificar o conjunto de bibliotecas (driver) que será utilizada: Oracle Driver, JDBC-ODBC Driver ou Sybase Driver.
- principais interfaces e a classe principal utilizadas para acesso ao banco de dados por meiodos padrões JDBC:

<div align="center">

Componente | Descrição
-----------|------------------
DriverManager | Responsável por encontrar o drive e estabelecer a conexão com o SGBD.
Conection | Representa a conexão com o SGBDR por onde serão passados os comandos SQL.
Statement<br>PreparedStatement<br>CallableStatement | Representa os registros de um Statement, PreparedStatement ou CallableStatement.

</div>

- as classes para manipulação de um banco de dados estão no `pacote java.sql`. 
- para conectar-se a um banco de bados (SGDB) é preciso solicitar a abertura de uma conexão com o banco de dados utilizando o Driver Manager, que é o gerenciador de drivers.
  - caso o DriverManager consiga estabelecer uma conexão com o SGDB, um `objeto do tipo java.sql.Connection` é retornado, caso contrário, uma exceção é gerada.
- quando uma implementação (driver) é carregada, é registrada utilizando o Driver Manager, a partir do qual serão criadas as conexões para a base de dados utilizando o `método getConnection()` (que recebe uma String que identifica o banco de dados que será conectado).
- após a conexão, é possível utilizar os objetos do tipo java.sql.Statement, java.sql.PreparedStatement e java.sql.CallableStatement para executar comandos SQL no SGDB.
- todas as interfaces e classes da estrutura do JDBC podem ser encontradas no `arquivo rt.jar`, contido no pacote JDK do Java.

> O desenvolvimento de sistemas que acessam banco de dados segue alguns passos comuns, independente da linguagem de programação utilizada.

### a) para a comunicação de um sistema a um BD:
  - primeiro, é necessário ter o “número” do banco de dados destinatário, considerando o endereço de IP (Internet Protocol) como endereço físico e a porta como endereço lógico.
  - com o banco disponível, obter uma conexão para realizar a comunicação.
  - por meio da conexão, é possível enviar comandos SQL, que serão executados no banco de dados.
  - por fim, a conexão é fechada, encerrando-se o processo.

### b) importante:
- deve ser realizado o tratamento dos possíveis problemas que podem ocorrer no processo da comunicação com o BD.
- o próprio programa deve prever e tratar as possíveis situações de erro.

## 1.4 Banco de dados Oracle e comandos SQL

### a) Criar a tabela para armazenar os dados dos colaboradores de uma empresa:
- A tabela deverá conter as colunas:
  - CODIGO_COLABORADOR: chave primária da tabela, campo obrigatório e com valores únicos. 
  - NOME: nome do colaborador. 
  - EMAIL: e-mail do funcionário. 
  - SALARIO: valor do salário do colaborador. 
  - DATA_CONTRATACAO: data de contratação.

> Para criar a tabela, podemos utilizar o comando SQL CREATE TABLE ou fazê-lo de forma visual, por meio do Oracle SQL Developer.

### b) Criar uma sequence para gerar os valores do código do colaborador.
- `sequence` é um objeto do banco de dados Oracle que gera sequências numéricas automaticamente.

## 1.4.1 Cadastrando informações na tabela

- utilizando o ***comando INSERT*** para cadastrar um registro em uma tabela. 
- podemos utilizá-lo de duas formas:
  - omitindo o nome das colunas e informando somente os valores para as colunas (os dados serão inseridos conforme a ordem das colunas na tabela) OU
  - informando os nomes das colunas e os valores que serão cadastrados. Nesse caso, cada valor será inserido na respectiva coluna, conforme a ordem estabelecida na instrução.

> O mais indicado é utilizar a segunda opção, pois caso a estrutura da tabela seja alterada, os valores ainda serão inseridos nas colunas corretas.

## 1.4.2 Leitura de dados de uma tabela

- para recuperar os registros de uma ou mais tabelas, utilizar o ***comando SELECT***.
- adicionar filtros às buscas, pois permitem recuperar os registros de acordo com condições, além de trazer registros mais específicos, e de utilizarem menos capacidade de processamento.
- para criar condições, precisamos utilizar os operadores relacionais e lógicos.

## 1.4.3 Atualizando valores na tabela

- utilizar o ***comando UPDATE***: permite a alteração do conteúdo de um ou mais campos (colunas) pertencentes a um ou mais registros (linhas) de uma tabela.
- é possível alterar várias colunas em um mesmo comando UPDATE, basta separar o nome das colunas por vírgula.

## 1.4.4 Remoção de registros de uma tabela (Delete)

- o ***comando DELETE*** permite remover um registro de uma tabela.
- precisamos especificar uma acondição, pois, sem ela, todos os registros da tabela serão apagados.

## 1.4.5 Conectando a base de dados

- no Eclipse, criar um novo projeto para manipular a base de dados: “File” > “New” > “Java Project”.
- configurar o ambiente (pois precisamos do driver JDBC do banco de dados Oracle). Logo, vamos adicionar o arquivo .jar ao projeto. Para isso: 
  - criar uma pasta chamada `lib` e adicionar o driver do Oracle (ojdbc11).
  - adicionar o driver no build path do projeto para que as classes e interfaces fiquem disponíveis para o uso dentro do projeto (botão direito do mouse no driver > “BuildPath” > “Add to Build Path).
- agora estamos prontos para começar a desenvolver um programa!!!

### para estabelecer uma conexão com a base de dados:
- precisamos criar um objeto do tipo Connection que representará a conexão. 
- depois, poderemos realizar qualquer operação (Cadastrar, Atualizar, Apagar e Buscar) na base de dados.
- exemplo de classe de teste que realiza a conexão com o banco de dados:

~~~java
package br.com.fiap.teste;
  
  import java.sql.Connection;
  import java.sql.DriverManager;
  import java.sql.SQLException;
  
  public class TesteView {
  
    public static void main(String[] args) {
      try {
        //Registra o Driver
        Class.forName("oracle.jdbc.driver.OracleDriver");
  
        //Abre uma conexão
        Connection conexao = DriverManager.getConnection(
            "jdbc:oracle:thin:@192.168.60.15:1521:ORCL", "OPS$PF0392", "123456");
        
        System.out.println("Conectado!");
        
        //Fecha a conexão
        conexao.close();
        
      //Tratamento de erro 
      } catch (SQLException e) {
        System.err.println("Não foi possível conectar no Banco de Dados");
        e.printStackTrace();
      } catch (ClassNotFoundException e) {
        System.err.println("O Driver JDBC não foi encontrado!");
        e.printStackTrace();
      }
    }
  }
~~~

## 1.4.6 Statements

- há três objetos do tipo Statement:
  - `Statement`: utilizado para executar um comando SQL estático. 
  - `Prepared Statement`: utilizado para executar um comando SQL que recebe um ou mais parâmetros. 
  - `Callable Statement`: utilizado para chamar stored procedures ou functions.
  
- os principais métodos dessas implementações são:
  - `executeUpdate`: executa um comando SQL (INSERT, UPDATE, DELETE) e retorna o número de linhas afetadas. 
  - `executeQuery`: executa um comando SQL (SELECT) e retorna o(s) resultado(s) por meio de um objeto do tipo ResultSet.

- para recuperar o objeto do tipo Statement, utilizamos o método createStatement(), da interface Connection.

### a) Inclusão:

~~~java
Statement stmt = conexao.createStatement();
  stmt.executeUpdate("INSERT INTO TAB_COLABORADOR(CODIGO_COLABORADOR, NOME, EMAIL, SALARIO, DATA_CONTRATACAO) VALUES (SQ_COLABORADOR.NEXTVAL, 'Leandro', 'leandro@gmail.com', 1500, TO_DATE('10/12/2009','dd/mm/yyyy'))");
~~~

### b) Alteração:

~~~java
Statement stmt = conexao.createStatement();
  stmt.executeUpdate("UPDATE TAB_COLABORADOR SET SALARIO = 5000 WHERE CODIGO_COLABORADOR = 1");
~~~

### c) Exclusão:

~~~java
Statement stmt = conexao.createStatement();
  stmt.executeUpdate("DELETE FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = 1");
~~~

### d) Busca:

~~~java
Statement stmt = conexao.createStatement();
  ResultSet rs = stmt.executeQuery("SELECT * FROM TAB_COLABORADOR");
~~~

> Nos exemplos acima, os comandos SQL são estáticos (os valores já estão definidos diretamente na string). Quando precisamos de comandos SQL configuráveis, devemos utilizar a interface `PreparedStatement`!

- assim, podemos parametrizar o comando SQL com o ponto de interrogação(?) por meio dos métodos set.
- também é possível atribuir valores a esses parâmetros, evitando ataques do tipo SQL Injection.
- é indicado utilizar o PreparedStatement para manipular a base de dados, sempre que possível, pois ele proporciona melhor performance e clareza do código-fonte.
- para obter o objeto PreparedStatement, utilizamos o método prepareStatement() da interface Connection.
- exemplo:

~~~java
PreparedStatement stmt = conexao.prepareStatement("INSERT INTO TAB_COLABORADOR(CODIGO_COLABORADOR, NOME, EMAIL, SALARIO, DATA_CONTRATACAO) VALUES (SQ_COLABORADOR.NEXTVAL, ?, ?, ?, ?)");
  stmt.setString(1, "Thiago"); //Primero parâmetro (Nome)
  stmt.setString(2, "thiago@gmail.com");//Segundo parâmetro (Email)
  stmt.setDouble(3, 5000); //Terceiro parâmetro (Salário)
  //Instancia um objeto do tipo java.sql.Date com a data atual
  java.sql.Date data = new java.sql.Date(new java.util.Date().getTime());
  stmt.setDate(4,data);//Quarto parâmetro (data contratação)
        
  stmt.executeUpdate();
~~~

> IMPORTANTE: no exemplo acima, no lugar dos dados dos parâmetros, foram adicionados `pontos de interrogação (?)` para que, posteriormente,informemos os respectivos valores por meio dos métodos set, que serão escolhidos de acordo com o tipo de dado. Esse método recebe dois parâmetros: o primeiro é a posição do ponto de interrogação (?), que se inicia em 1, e o segundo é o valor que será atribuído a essa posição.

- para cada uma das operações em SQL, é possível utilizar o PreparedStatement:

### a) Alteração:

~~~java
PreparedStatement stmt = conexao.prepareStatement("UPDATE TAB_COLABORADOR SET SALARIO = ? WHERE CODIGO_COLABORADOR = ?");
  stmt.setDouble(1, 5000);
  stmt.setInt(2, 100);
  stmt.executeUpdate();
~~~

### b) Exclusão:

~~~java
PreparedStatement stmt = conexao.prepareStatement("DELETE FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = ?");
~~~

### c) Busca:

~~~java
PreparedStatement stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR WHERE NOME = ?");
  stmt.setString(1, "Thiago");
  ResultSet result = stmt.executeQuery();
~~~

## 1.4.7 ResultSet

- a interface ResultSet é responsável pelo conjunto de registros retornados de um comando SELECT do SQL.
- permite navegar por seus registros de forma sequencial. Dessa forma, precisamos ***chamar o método next*** para mover o cursor para o próximo registro.
  - esse método retorna false quando não conseguir ir para o próximo registro, caracterizando o final dos registros. 
  - as colunas do registro podem ser acessadas por meio de um índice que representa a posição da coluna (inicia em 1) ou por meio do próprio nome da coluna.
- ***principais métodos***:
  - `next`: move o cursor para a próxima linha.
  - `getInt`: retorna os dados da coluna designada como int do Java.
  - `getString`: retorna os dados da coluna designada como uma String do Java.
  - `getBoolean`: retorna os dados da coluna designada como boolean do Java.
  - `getDouble`: retorna os dados da coluna designada como double do Java.

Exemplo:

~~~java
import java.sql.Connection;
  import java.sql.DriverManager;
  import java.sql.PreparedStatement;
  import java.sql.ResultSet;
  import java.sql.SQLException;
  
  public class TesteView {
  
    public static void main(String[] args) {
      try {
    //Registra o Driver
    Class.forName("oracle.jdbc.driver.OracleDriver");
  
    //Abre uma conexão
    Connection conexao = DriverManager.getConnection(
  "jdbc:oracle:thin:@oracle.fiap.com.br:1521:ORCL", "OPS$PF0392", "123456");
        
    System.out.println("Conectado!");
        
  PreparedStatement stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR WHERE NOME = ?");
    stmt.setString(1, "Thiago");
    ResultSet result = stmt.executeQuery();
        
    //Percorre todos os registros encontrados
    while (result.next()){
      //Recupera os valores de cada coluna
      int codigo = result.getInt("CODIGO_COLABORADOR");
      String nome = result.getString("NOME");
      String email = result.getString("EMAIL");
      double salario = result.getDouble("SALARIO");
      java.sql.Date data = result.getDate("DATA_CONTRATACAO");
      //Exibe as informações do registro
      System.out.println(codigo + " " + nome + " " + email + " " + salario + " " + data);
  }
        
    //Fecha a conexão
    conexao.close();
        
    //Tratamento de erro  
    } catch (SQLException e) {
      System.err.println("Não foi possível conectar no Banco de Dados");
      e.printStackTrace();
    } catch (ClassNotFoundException e) {
      System.err.println("O Driver JDBC não foi encontrado!");
      e.printStackTrace();
    }
  }
  }
~~~

## 1.4.8 CallableStatement

- utilizado para chamar stored procedures ou functions de forma padronizada para todas as bases de dados.
- é possível chamar uma stored procedure utilizando ou não o parâmetro de resultado.

### a) sintaxe básica para chamada de stored procedure com parâmetro de resultado:

~~~java
CallableStatement cs = conexao.prepareCall("{call proc(?)}");
~~~

### b) sem parâmetro de resultado:

~~~java
CallableStatement cs = conexao.prepareCall("{call proc()}");
~~~

- para definir os parâmetros de entrada, utilizamos o mesmo padrão do PreparedStatement, e os parâmetros de saída são definidos por meio do método registerOutParameter.

~~~java
//Cria o CallableStatement
  CallableStatement cs = conexao.prepareCall("{call SP_Contar_Colaboradores(?,?)}");
        
  //Define o tipo do parâmetro de saída (primeiro ?)
  cs.registerOutParameter(1, java.sql.Types.INTEGER);
        
  //Define o valor do parâmetro de entrada (segundo ?)
  cs.setDouble(2, 1500);
        
  //Executa a procedure
  cs.executeUpdate();
        
  //Recupera o valor do parâmetro de saída
  int total = cs.getInt(1);
  System.out.println("Total de colaboradores com salário maior que 1500: " + total);
~~~

- exemplo de Stored Procedure que retorna o resultado de um SELECT:

~~~java
//Cria o CallableStatement
  CallableStatement cs = conexao.prepareCall("{call SP_Retornar_Todos_Colaboradores(?,?)}");
        
  //Define o valor do parâmetro de entrada 
  cs.setDouble(1,1500);
  
  //Define o tipo do parâmetro de saída
  cs.registerOutParameter(2, OracleTypes.CURSOR);
        
  //Executa a procedure
  cs.execute();
        
  //Recupera o valor do parâmetro de saída
  ResultSet cursor = (ResultSet) cs.getObject(2);
        
  //Percorre todos os registros encontrados
  while (cursor.next()){
    //Recupera os valores de cada coluna
    int codigo = cursor.getInt("CODIGO_COLABORADOR");
    String nome = cursor.getString("NOME");
    System.out.println(codigo + " " + nome);
  }
~~~

---

<div align="center">
<h2>Implementando o exemplo</h2>
</div>

## 1. Começar desenvolvendo o Java Bean Colaborador:
- essa classe irá representar a nossa tabela do banco de dados, devendo possuir atributos que representam cada coluna da tabela. 
- utilizaremos o encapsulamento, deixando os atributos com o modificador de acesso private, e disponibilizaremos os métodos assessores (gets e sets). 
- implementaremos o construtor padrão e com parâmetros.
- para armazenar a data de contratação, utilizamos a classe java.util.Calendar. 

> Essa classe possui grande importância por facilitar o processo de passagem de valores do banco de dados para a aplicação Java e vice-versa.

~~~java
package br.com.fiap.bean;

import java.util.Calendar;

public class Colaborador {

	private int codigo;
	private String nome;
	private String email;
	private double salario;
	private Calendar dataContratacao;
	
	public Colaborador(int codigo, String nome, String email, double salario, Calendar dataContratacao) {
		super();
		this.codigo = codigo;
		this.nome = nome;
		this.email = email;
		this.salario = salario;
		this.dataContratacao = dataContratacao;
	}
	
	public Colaborador() {
		super();
	}
	
	public int getCodigo() {
		return codigo;
	}
	
	public void setCodigo(int codigo) {
		this.codigo = codigo;
	}
	
	public String getNome() {
		return nome;
	}
	
	public void setNome(String nome) {
		this.nome = nome;
	}
	
	public String getEmail() {
		return email;
	}
	
	public void setEmail(String email) {
		this.email = email;
	}
	
	public double getSalario() {
		return salario;
	}
	
	public void setSalario(double salario) {
		this.salario = salario;
	}
	
	public Calendar getDataContratacao() {
		return dataContratacao;
	}
	
	public void setDataContratacao(Calendar dataContratacao) {
		this.dataContratacao = dataContratacao;
	}	
}
~~~

## 2. Criar uma classe que será responsável por fornecer uma conexão com o BD:
- para cada operação no banco dados (INSERT, UPDATE, SELECT e DELETE),foi necessário primeiro obter uma conexão. 
- com essa classe, não vamos precisar escrever códigos repetidos, utilizando os conceitos de orientação a objetos.

> Essa classe possui somente um método estático que cria e retorna uma conexão com o banco. O método é estático para que a classe não precise de uma instância para ser invocada, bastando referenciá-la por meio do nome da classe: `EmpresaDBManager.obterConexao()`.

~~~java
package br.com.fiap.jdbc;
  
  import java.sql.Connection;
  import java.sql.DriverManager;
  
  public class EmpresaDBManager {
  
    public static Connection obterConexao() {
      Connection conexao = null;
      try {
        Class.forName("oracle.jdbc.driver.OracleDriver");
  
        conexao = DriverManager.getConnection(
            "jdbc:oracle:thin:@oracle.fiap.com.br:1521:ORCL",
            "OPS$XXXX", "XXXXX");
  
      } catch (Exception e) {
        e.printStackTrace();
      }
      return conexao;
    }
  
  }
~~~

## 3. Desenvolver a classe ColaboradorDAO, responsável pela manipulação da tabela TAB_COLABORADOR.
- a classe possui essa nomenclatura pois segue um padrão de projeto chamado DAO (`Data Access Object`), responsável pelo código de acesso aos dados, centralizando a implementação dessa responsabilidade no projeto. 
- a classe DAO deve terum atributo para armazenar o objeto que representa a conexão com o BD.

~~~java
package br.com.fiap.dao;
  
  public class ColaboradorDAO {
  
    private Connection conexao;
  
  }
~~~

- desenvolver o primeiro método, que será responsável por cadastrar um colaborador.
- para isso, ele deve receber um objeto do tipo Colaborador para ser inserido no banco:

~~~java
public class ColaboradorDAO {
    
      private Connection conexao;
    
      public void cadastrar(Colaborador colaborador) {
        PreparedStatement stmt = null;
    
        try {
          conexao = EmpresaDBManager.obterConexao();
          String sql = "INSERT INTO TAB_COLABORADOR(CODIGO_COLABORADOR, NOME, EMAIL, SALARIO, DATA_CONTRATACAO) VALUES (SQ_COLABORADOR.NEXTVAL, ?, ?, ?, ?)";
          stmt = conexao.prepareStatement(sql);
          stmt.setString(1, colaborador.getNome());
          stmt.setString(2, colaborador.getEmail());
          stmt.setDouble(3, colaborador.getSalario());
          java.sql.Date data = new java.sql.Date(colaborador.getDataContratacao().getTimeInMillis());
          stmt.setDate(4, data);
    
          stmt.executeUpdate();
        } catch (SQLException e) {
          e.printStackTrace();
        } finally {
          try {
            stmt.close();
            conexao.close();
          } catch (SQLException e) {
            e.printStackTrace();
          }
        }
      }
    }
~~~

- não se esquecer dos imports! 
- um atalho do eclipse é o CTRL + SHIFT + o para fazer o import automático.

~~~java
import java.sql.Connection;
  import java.sql.PreparedStatement;
  import java.sql.SQLException;
  
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.jdbc.EmpresaDBManager;
~~~

## 4. Desenvolver uma classe de teste para verificar se está tudo correto.
- criar uma classe com o método main:

> Essa classe cria uma instância da classe ColaboradorDAO e do Colaborador e, por meio do método cadastrar do ColaboradorDAO, é realizado o cadastro no banco de dados.

~~~java
package br.com.fiap.teste;
  
  import java.util.Calendar;
  
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.dao.ColaboradorDAO;
  
  public class TesteCadastro {
  
    public static void main(String[] args) {
      //Instancia o DAO
      ColaboradorDAO dao = new ColaboradorDAO();
  
      //Instancia o Colaborador
      Colaborador colaborador = new Colaborador();
      colaborador.setNome("Pedro");
      colaborador.setEmail("pedro@fiap.com.br");
      colaborador.setSalario(5000);
      colaborador.setDataContratacao(Calendar.getInstance());
  
      //Cadastra no banco de dados
      dao.cadastrar(colaborador);
  
      System.out.println("Cadastrado!");
    }
  
  }
~~~

## 5. Implementar a próxima funcionalidade no DAO: listar.
- voltar à classe ColaboradorDAO e criar o novo método.

> Esse método retorna uma lista comtodos os colaboradores cadastrados. Não se esqueça de adicionar os imports do List, ArrayList e ResultSet.

- para cada registro no ResultSet, é instanciado um objeto Colaborador para armazenar as informações encontradas. Esse objeto é adicionado à lista que será retornada.

~~~java
public List<Colaborador> listar() {
    //Cria uma lista de colaboradores
    List<Colaborador> lista = new ArrayList<Colaborador>();
    PreparedStatement stmt = null;
    ResultSet rs = null;
    try {
      conexao = EmpresaDBManager.obterConexao();
    stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR");
    rs = stmt.executeQuery();
  
    //Percorre todos os registros encontrados
    while (rs.next()) {
    int codigo = rs.getInt("CODIGO_COLABORADOR");
    String nome = rs.getString("NOME");
        String email = rs.getString("EMAIL");
        double salario = rs.getDouble("SALARIO");
        java.sql.Date data = rs.getDate("DATA_CONTRATACAO");
        Calendar dataContratacao = Calendar.getInstance();
        dataContratacao.setTimeInMillis(data.getTime());
        //Cria um objeto Colaborador com as informações encontradas
        Colaborador colaborador = new Colaborador(codigo, nome, email, salario, dataContratacao);
        //Adiciona o colaborador na lista
        lista.add(colaborador);
      }
    } catch (SQLException e) {
      e.printStackTrace();
    }finally {
      try {
        stmt.close();
        rs.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
    return lista;
  }
~~~
## 6. Criação de uma classe de teste para listagem.
- essa classe irá instanciar o ColaboradorDAO e chamar o método listar() para receber a lista de colaboradores cadastrados no banco de dados.
- implementado um laço de repetição foreach para percorrer toda a lista e imprimir os valores dos atributos do colaborador.

~~~java
package br.com.fiap.teste;
  
  import java.util.List;
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.dao.ColaboradorDAO;
  
  public class TesteListagem {
  
    public static void main(String[] args) {
  
      ColaboradorDAO dao = new ColaboradorDAO();
      
      List&lt;Colaborador> lista = dao.listar();
      for (Colaborador item : lista) {
        System.out.println(item.getCodigo() + " " + item.getNome() + " " + item.getEmail() + " " + item.getSalario() + " " + item.getDataContratacao().getTime());
      }
    }
    
  }
~~~

## 7. Implementando a funcionalidade para remover um colaborador do BD.
- esse método, que deve ser implementado na classe ColaboradorDAO, recebe o código do colaborador, que será excluído do banco de dados.

~~~java
public void remover(int codigo){
    PreparedStatement stmt = null;
  
    try {
      conexao = EmpresaDBManager.obterConexao();
      String sql = "DELETE FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = ?";
      stmt = conexao.prepareStatement(sql);
      stmt.setInt(1, codigo);
      stmt.executeUpdate();
    } catch (SQLException e) {
      e.printStackTrace();
    } finally {
      try {
        stmt.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
  }
~~~

## 8. Criação de uma nova Classe para testes.
- a classe de teste instancia o ColaboradorDAO para chamar o método remover, passando o ID do colaborador que será excluído do banco de dados.

~~~java
package br.com.fiap.teste;
  
  import br.com.fiap.dao.ColaboradorDAO;
  
  public class TesteRemocao {
  
    public static void main(String[] args) {
      ColaboradorDAO dao = new ColaboradorDAO();
      //Remove o colaborador com código 1
      dao.remover(1);
    }
}
~~~

## 9. Implementar o método para buscar por código, para posteriormente implementar o método de atualização.

- para finalizar o CRUD, implementar o método de atualização. P
- porém, antes desenvolver o método buscar por código, para recuperar colaborador que será atualizado.
- na classe ColaboradorDAO, adicionar o método buscarPorId, que recebe o código do colaborador.

~~~java
Colaborador colaborador = null;
  PreparedStatement stmt = null;
  ResultSet rs = null;
  try {
    conexao = EmpresaDBManager.obterConexao();
    stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = ?");
    stmt.setInt(1, codigoBusca);
    rs = stmt.executeQuery();
  
    if (rs.next()){
      int codigo = rs.getInt("CODIGO_COLABORADOR");
      String nome = rs.getString("NOME");
      String email = rs.getString("EMAIL");
      double salario = rs.getDouble("SALARIO");
      java.sql.Date data = rs.getDate("DATA_CONTRATACAO");
      Calendar dataContratacao = Calendar.getInstance();
      dataContratacao.setTimeInMillis(data.getTime());
      colaborador = new Colaborador(codigo, nome, email, salario, dataContratacao);
    }
    
  } catch (SQLException e) {
    e.printStackTrace();
  }finally {
    try {
      stmt.close();
      rs.close();
      conexao.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
  return colaborador;
~~~

- após a execução da query, é acionado o método next() do ResultSetpara verificar se existe algum registro.
- em caso positivo, são recuperados todos os valores do registro e instanciado um Colaborador para armazenar essas informações.

### 10. Implementando método de atualização

~~~java
public void atualizar(Colaborador colaborador){
    PreparedStatement stmt = null;
  
    try {
      conexao = EmpresaDBManager.obterConexao();
      String sql = "UPDATE TAB_COLABORADOR SET NOME = ?, EMAIL = ?, SALARIO = ?, DATA_CONTRATACAO = ? WHERE CODIGO_COLABORADOR = ?";
      stmt = conexao.prepareStatement(sql);
      stmt.setString(1, colaborador.getNome());
      stmt.setString(2, colaborador.getEmail());
      stmt.setDouble(3, colaborador.getSalario());
      java.sql.Date data = new java.sql.Date(colaborador.getDataContratacao().getTimeInMillis());
      stmt.setDate(4, data);
      stmt.setInt(5, colaborador.getCodigo());
  
      stmt.executeUpdate();
    } catch (SQLException e) {
      e.printStackTrace();
    } finally {
      try {
        stmt.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
  }
~~~

- para realizar a atualização dos dados de um colaborador, primeiro a classe de teste deve recuperar o registro, utilizando o método buscarPorId, depois os valores dos dados que serão alterados devem ser informados e, por último, o método atualizar deve ser invocado.

~~~java
package br.com.fiap.teste;
  
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.dao.ColaboradorDAO;
  
  public class TesteAlteracao {
  
    public static void main(String[] args) {
  
      ColaboradorDAO dao = new ColaboradorDAO();
      //Recupera o colaborador com código 1
      Colaborador colaborador = dao.buscarPorId(1);
      //Imprime os valores do colaborador
      System.out.println(colaborador.getCodigo() + " "
          + colaborador.getNome() + " " + colaborador.getEmail() + " "
          + colaborador.getSalario() + " "
          + colaborador.getDataContratacao().getTime());
      //Altera os valores de alguns atributos do colaborador
      colaborador.setSalario(1500);
      colaborador.setEmail("teste@fiap.com.br");
      //Atualiza no banco de dados
      dao.atualizar(colaborador);
    }
  
  }
~~~

---

<div align="center">
<h2>2. CONTROLE TRANSACIONAL</h2>
</div>

- toda comunicação com banco de dados requer cuidados com acessos paralelos e integridade dos dados.
- todo SGBD e as linguagensde programação possuem tratamento específico para permitir a segurança e integridade dos dados, assim como no JDBC.

## 2.1 Transação

- é uma unidade que preserva a consistência de informações no banco de dados.
- são unidades atômicas de operações; em ciência da computação, uma transação atômica é uma operação, ou conjunto de operações, em uma base de dados, ou em qualquer outro sistema computacional, que deve ser executada completamente em caso de sucesso, ou ser abortada completamente em caso de erro.
- uma transação pode ser representada pela ***sigla ACID***:
  - `Atomicidade` (Atomicity): atômico, tudo (commit) ou nada (rollback). 
  - `Consistência` (Consistency): toda transação executada deve seguir as regras de integridade do banco de dados, mantendo a consistência da base de dados. 
  - `Isolamento` (Isolation): garante que nenhuma transação seja interferida por outra até que a primeira seja completada. 
  - `Durabilidade` (Durability): garante que as informações gravadas no banco de dados durem de forma imutável até que outra transação de atualização ou remoção asafetem.
- as ***operações possíveis*** para o controle transacional são: 
  - `Commit`: todas as operações envolvidas em uma unidade de processo executam com sucesso, efetivando assim as alterações na base de dados.
  - `Rollback`: todas as operações envolvidas em uma unidade de processo não executam corretamente, não efetuando assim as operações das transações na base de dados.

> Por padrão, toda conexão com JDBC está configurada para realizar o COMMIT automaticamente, após a execução de um comando SQL. Para desabilitar essa configuração, utilizamos o `método setAutoCommit(false)`, da interface Connection.

~~~java
try {
    //Desabilita o autocommit
    conexao.setAutoCommit(false);
    
    //Primeira transação - Atualiza o salário
    PreparedStatement stmt = conexao.prepareStatement("UPDATE TAB_COLABORADOR SET SALARIO = ? WHERE CODIGO_COLABORADOR = ?");
    stmt.setDouble(1, 5000);
    stmt.setInt(2, 1);
    stmt.executeUpdate();
    
    //Segunda transação - Atualiza o e-mail
    PreparedStatement stmt2 = conexao.prepareStatement("UPDATE TAB_COLABORADOR SET EMAIL = ? WHERE CODIGO_COLABORADOR = ?");
    stmt2.setString(1, "teste@teste.com.br");
    stmt2.setInt(2, 1);
    stmt2.executeUpdate();
    
    //Efetiva as duas transações
    conexao.commit();
  
  } catch (SQLException se) {
    //Não efetiva as duas transações
    conexao.rollback();
}
~~~

- no código acima, se ocorrer algum erro, o comando conexao.rollback()será executado para desfazer as transações e, assim, não modificar as informações do BD.

## 2.2 Design patterns (Padrão de Projeto de Software)

- descreve uma solução geral reutilizável para um problema recorrente no desenvolvimento de sistemas. 
- não é um código final, é uma descrição ou modelo de como resolver o problema que ocorre em vários sistemas de diferentes áreas de atuação ou plataforma de desenvolvimento.
- livro "Design Patterns: Elements of Resuable Object-Oriented Software".
- ***vantagens***:
  - `Facilidade de comunicação`: os padrões possuem nomes, os quais descrevem uma solução que deve ser de conhecimento comum entre os desenvolvedores. 
  - `Credibilidade`: padrões de projetos são utilizados constantemente nas implementações de sistemas; são amplamente testadas e aprovadas. 
  - `Facilidade de manutenção`: Padrões de projetos tendem a reduzir o acoplamento entre os componentes, o que facilita a manutenção de um sistema.
- **principais Design Patterns para implementação do backendde um sistema:**

### 2.2.1 Data Access Object (DAO)

- esse padrão de projeto abstrai e encapsula todo o acesso à base de dados.
- a ideia é criar uma classe Java que separa totalmente a lógica de acesso e manipulação de dados da aplicação.
- é a camada que separa a aplicação do banco de dados: possui todo o código de acesso ao banco de dados, tornando mais fáceis os testes e a manutenção.
- OU SEJA, devemos desenvolver uma classe DAO para cada entidade, a fim de separar a responsabilidade do acesso à base de dados da entidade a seus respectivos DAOs.
- exemplo:

~~~java
package br.com.fiap.dao;
  
  import java.sql.Connection;
  import java.sql.PreparedStatement;
  import java.sql.ResultSet;
  import java.sql.SQLException;
  import java.util.ArrayList;
  import java.util.Calendar;
  import java.util.List;
  
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.jdbc.EmpresaDBManager;
  
  public class ColaboradorDAO {
  
  private Connection conexao;
  
  public void cadastrar(Colaborador colaborador) {
    PreparedStatement stmt = null;
  
    try {
      conexao = EmpresaDBManager.obterConexao();
      String sql = "INSERT INTO TAB_COLABORADOR(CODIGO_COLABORADOR, NOME, EMAIL, SALARIO, DATA_CONTRATACAO) VALUES (SQ_COLABORADOR.NEXTVAL, ?, ?, ?, ?)";
      stmt = conexao.prepareStatement(sql);
      stmt.setString(1, colaborador.getNome());
      stmt.setString(2, colaborador.getEmail());
      stmt.setDouble(3, colaborador.getSalario());
      java.sql.Date data = new java.sql.Date(colaborador.getDataContratacao().getTimeInMillis());
      stmt.setDate(4, data);
  
      stmt.executeUpdate();
    } catch (SQLException e) {
      e.printStackTrace();
    } finally {
      try {
        stmt.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
  } 
  
  public List<Colaborador> listar() {
    //Cria uma lista de colaboradores
    List<Colaborador> lista = new ArrayList<Colaborador>();
    PreparedStatement stmt = null;
    ResultSet rs = null;
    try {
      conexao = EmpresaDBManager.obterConexao();
      stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR");
      rs = stmt.executeQuery();
  
      //Percorre todos os registros encontrados
      while (rs.next()) {
        int codigo = rs.getInt("CODIGO_COLABORADOR");
        String nome = rs.getString("NOME");
        String email = rs.getString("EMAIL");
        double salario = rs.getDouble("SALARIO");
        java.sql.Date data = rs.getDate("DATA_CONTRATACAO");
        Calendar dataContratacao = Calendar.getInstance();
        dataContratacao.setTimeInMillis(data.getTime());
        //Cria um objeto Colaborador com as informações encontradas
        Colaborador colaborador = new Colaborador(codigo, nome, email, salario, dataContratacao);
        //Adiciona o colaborador na lista
        lista.add(colaborador);
      }
    } catch (SQLException e) {
      e.printStackTrace();
    }finally {
      try {
        stmt.close();
        rs.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
    return lista;
  }
  
  public void atualizar(Colaborador colaborador){
    PreparedStatement stmt = null;
  
    try {
      conexao = EmpresaDBManager.obterConexao();
      String sql = "UPDATE TAB_COLABORADOR SET NOME = ?, EMAIL = ?, SALARIO = ?, DATA_CONTRATACAO = ? WHERE CODIGO_COLABORADOR = ?";
      stmt = conexao.prepareStatement(sql);
      stmt.setString(1, colaborador.getNome());
      stmt.setString(2, colaborador.getEmail());
      stmt.setDouble(3, colaborador.getSalario());
      java.sql.Date data = new java.sql.Date(colaborador.getDataContratacao().getTimeInMillis());
      stmt.setDate(4, data);
      stmt.setInt(5, colaborador.getCodigo());
  
      stmt.executeUpdate();
    } catch (SQLException e) {
      e.printStackTrace();
    } finally {
      try {
        stmt.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
  }
  
  public void remover(int codigo){
    PreparedStatement stmt = null;
  
    try {
      conexao = EmpresaDBManager.obterConexao();
      String sql = "DELETE FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = ?";
      stmt = conexao.prepareStatement(sql);
      stmt.setInt(1, codigo);
      stmt.executeUpdate();
    } catch (SQLException e) {
      e.printStackTrace();
    } finally {
      try {
        stmt.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
  }
  
  public Colaborador buscarPorId(int codigoBusca){
    Colaborador colaborador = null;
    PreparedStatement stmt = null;
    ResultSet rs = null;
    try {
      conexao = EmpresaDBManager.obterConexao();
      stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = ?");
      stmt.setInt(1, codigoBusca);
      rs = stmt.executeQuery();
  
      if (rs.next()){
        int codigo = rs.getInt("CODIGO_COLABORADOR");
        String nome = rs.getString("NOME");
        String email = rs.getString("EMAIL");
        double salario = rs.getDouble("SALARIO");
        java.sql.Date data = rs.getDate("DATA_CONTRATACAO");
        Calendar dataContratacao = Calendar.getInstance();
        dataContratacao.setTimeInMillis(data.getTime());
        colaborador = new Colaborador(codigo, nome, email, salario, dataContratacao);
      }
      
    } catch (SQLException e) {
      e.printStackTrace();
    }finally {
      try {
        stmt.close();
        rs.close();
        conexao.close();
      } catch (SQLException e) {
        e.printStackTrace();
      }
    }
    return colaborador;
  }
}
~~~

- para utilizar o DAO, basta instanciar a classe e invocar os seus métodos:

~~~java
public static void main(String[] args) {
  ColaboradorDAO dao = new ColaboradorDAO();
  List<Colaborador> lista = dao.listar();
}
~~~

- outra ***boa prática na implementação do padrão de projeto DAO*** é a utilização de ***interfaces***: a aplicação pode referenciar a interface em vez da classe, diminuindo acoplamento. 
- utilizar interface permite a criação de diferentes implementações que podem ser trocadas sem a necessidade de grandes alterações no código da camada de negócio ou apresentação.
- exemplo da implementação do ColaboradorDAO, utilizando uma interface e a implementação para o banco de dados Oracle:

~~~java
// Interface que define as funcionalidades do DAO:

package br.com.fiap.dao;
  
  import java.util.List;
  import br.com.fiap.bean.Colaborador;
  
  public interface ColaboradorDAO {
  
    public void cadastrar(Colaborador colaborador);
    public List<Colaborador> listar();
    public void atualizar(Colaborador colaborador);
    public void remover(int codigo);
    public Colaborador buscarPorId(int codigoBusca);
}
~~~

~~~java
// Classe que implementa as funcionalidades definidas na interface:

package br.com.fiap.dao;
  
  import java.sql.Connection;
  import java.sql.PreparedStatement;
  import java.sql.ResultSet;
  import java.sql.SQLException;
  import java.util.ArrayList;
  import java.util.Calendar;
  import java.util.List;
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.jdbc.EmpresaDBManager;
  
  public class OracleColaboradorDAO implements ColaboradorDAO {
  
    private Connection conexao;
  
    public void cadastrar(Colaborador colaborador) {
      PreparedStatement stmt = null;
  
      try {
        conexao = EmpresaDBManager.obterConexao();
        String sql = "INSERT INTO TAB_COLABORADOR(CODIGO_COLABORADOR, NOME, EMAIL, SALARIO, DATA_CONTRATACAO) VALUES (SQ_COLABORADOR.NEXTVAL, ?, ?, ?, ?)";
        stmt = conexao.prepareStatement(sql);
        stmt.setString(1, colaborador.getNome());
        stmt.setString(2, colaborador.getEmail());
        stmt.setDouble(3, colaborador.getSalario());
        java.sql.Date data = new java.sql.Date(colaborador.getDataContratacao().getTimeInMillis());
        stmt.setDate(4, data);
  
        stmt.executeUpdate();
      } catch (SQLException e) {
        e.printStackTrace();
      } finally {
        try {
          stmt.close();
          conexao.close();
        } catch (SQLException e) {
          e.printStackTrace();
        }
      }
    } 
  
    public List&lt;Colaborador> listar() {
      //Cria uma lista de colaboradores
      List&lt;Colaborador> lista = new ArrayList&lt;Colaborador>();
      PreparedStatement stmt = null;
      ResultSet rs = null;
      try {
        conexao = EmpresaDBManager.obterConexao();
        stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR");
        rs = stmt.executeQuery();
  
        //Percorre todos os registros encontrados
        while (rs.next()) {
          int codigo = rs.getInt("CODIGO_COLABORADOR");
          String nome = rs.getString("NOME");
          String email = rs.getString("EMAIL");
          double salario = rs.getDouble("SALARIO");
          java.sql.Date data = rs.getDate("DATA_CONTRATACAO");
          Calendar dataContratacao = Calendar.getInstance();
          dataContratacao.setTimeInMillis(data.getTime());
          //Cria um objeto Colaborador com as informações encontradas
          Colaborador colaborador = new Colaborador(codigo, nome, email, salario, dataContratacao);
          //Adiciona o colaborador na lista
          lista.add(colaborador);
        }
      } catch (SQLException e) {
        e.printStackTrace();
      }finally {
        try {
          stmt.close();
          rs.close();
          conexao.close();
        } catch (SQLException e) {
          e.printStackTrace();
        }
      }
      return lista;
    }
  
    public void atualizar(Colaborador colaborador){
      PreparedStatement stmt = null;
  
      try {
        conexao = EmpresaDBManager.obterConexao();
        String sql = "UPDATE TAB_COLABORADOR SET NOME = ?, EMAIL = ?, SALARIO = ?, DATA_CONTRATACAO = ? WHERE CODIGO_COLABORADOR = ?";
        stmt = conexao.prepareStatement(sql);
        stmt.setString(1, colaborador.getNome());
        stmt.setString(2, colaborador.getEmail());
        stmt.setDouble(3, colaborador.getSalario());
        java.sql.Date data = new java.sql.Date(colaborador.getDataContratacao().getTimeInMillis());
        stmt.setDate(4, data);
        stmt.setInt(5, colaborador.getCodigo());
  
        stmt.executeUpdate();
      } catch (SQLException e) {
        e.printStackTrace();
      } finally {
        try {
          stmt.close();
          conexao.close();
        } catch (SQLException e) {
          e.printStackTrace();
        }
      }
    }
  
    public void remover(int codigo){
      PreparedStatement stmt = null;
  
      try {
        conexao = EmpresaDBManager.obterConexao();
        String sql = "DELETE FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = ?";
        stmt = conexao.prepareStatement(sql);
        stmt.setInt(1, codigo);
        stmt.executeUpdate();
      } catch (SQLException e) {
        e.printStackTrace();
      } finally {
        try {
          stmt.close();
          conexao.close();
        } catch (SQLException e) {
          e.printStackTrace();
        }
      }
    }
  
    public Colaborador buscarPorId(int codigoBusca){
      Colaborador colaborador = null;
      PreparedStatement stmt = null;
      ResultSet rs = null;
      try {
        conexao = EmpresaDBManager.obterConexao();
        stmt = conexao.prepareStatement("SELECT * FROM TAB_COLABORADOR WHERE CODIGO_COLABORADOR = ?");
        stmt.setInt(1, codigoBusca);
        rs = stmt.executeQuery();
  
        if (rs.next()){
          int codigo = rs.getInt("CODIGO_COLABORADOR");
          String nome = rs.getString("NOME");
          String email = rs.getString("EMAIL");
          double salario = rs.getDouble("SALARIO");
          java.sql.Date data = rs.getDate("DATA_CONTRATACAO");
          Calendar dataContratacao = Calendar.getInstance();
          dataContratacao.setTimeInMillis(data.getTime());
          colaborador = new Colaborador(codigo, nome, email, salario, dataContratacao);
        }
        
      } catch (SQLException e) {
        e.printStackTrace();
      }finally {
        try {
          stmt.close();
          rs.close();
          conexao.close();
        } catch (SQLException e) {
          e.printStackTrace();
        }
      }
      return colaborador;
    }
    
}
~~~

### 2.3 DAO Factory

- "fábrica de DAOs" para um tipo específico de banco de dados.
- esse padrão de projetos é recomendado quando não há previsão de mudar o banco de dados da aplicação (exemplo: se o sistema utiliza o banco de dados MySQL e não há previsão de trocar o banco). 
- a ideia do DAO Factory é centralizar a criação dos objetos DAOs: se a aplicação precisar de um objeto ColaboradorDAO, o DAO Factory irá provê-lo por meio de um método estático. 
- exemplo de implementação do DAO Factory, que está em uma aplicação que possui dois DAOs. Primeiro, vamos implementar os DAOs do Colaborador e do Cargo:

~~~java
public interface CargoDAO {
  public List<Cargo> listar();
  public void cadastrar(Cargo cargo);
}
    
public class OracleCargoDAO implements CargoDAO {}
  @Override
  public List<Cargo> listar() {
    //Implementação
  }

  @Override
  public void cadastrar(Cargo cargo) {
    //Implementação
    
  }
~~~

- Interface ColaboradorDAO e classe OracleColaboradorDAO, que implementa a interface:

~~~java
public interface ColaboradorDAO {
  public List<Colaborador> listar();
  public void cadastrar(Colaborador colaborador);
  }

  public class OracleColaboradorDAO implements ColaboradorDAO {
    public List<Colaborador> listar(){
      //Implementação
    }
    public void cadastrar(Colaborador colaborador){
      //Implementação
    }
  }
~~~

- Aagora vamos implementar o DAO Factory, a fábrica que fornece as instâncias dos DAO:

~~~java
package br.com.fiap.factory;
  
  import br.com.fiap.dao.CargoDAO;
  import br.com.fiap.dao.ColaboradorDAO;
  import br.com.fiap.dao.OracleCargoDAO;
  import br.com.fiap.dao.OracleColaboradorDAO;
  
  public abstract class DAOFactory {
    public static CargoDAO getCargoDAO(){
      return new OracleCargoDAO();
    }
    
    public static ColaboradorDAO getColaboradorDAO(){
      return new OracleColaboradorDAO();
    } 
  }
~~~

- a classe acima possui dois métodos estáticos que fornecem as instâncias dos DAOs. Para sua utilização, basta invocar esses métodos:

~~~java
import java.util.List;
  
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.dao.ColaboradorDAO;
  import br.com.fiap.factory.DAOFactory;
  
  public class TesteDAOFactory {
    public static void main(String[] args) {
      ColaboradorDAO dao = DAOFactory.getColaboradorDAO();
      List<Colaborador> lista = dao.listar();
    }
  }
~~~

### 2.3.1 Abstract Factory

- indicado quando é preciso suportar vários bancos de dados, pois permite criar implementações de DAOs para cada banco e prover o DAO correto, conforme a necessidade.
- a implementação desse padrão de projetos ***começa pelos DAOs*** (se a aplicação precisa suportar o Oracle e o SQL Server, por exemplo, é necessário criar uma interface e implementá-la em duas classes: uma específica, que acessa BD Oracle, e outra que acessa o banco de dados SQL Server.), ***e em seguida, devemos implementar a Fábrica de DAOs***, uma classe abstrata (não pode ser instanciada), e que deve possuir um método estático que retorna uma instância da Fábrica de DAO de acordo com o Banco de dados escolhido.
- após definirmos as interfaces do DAO (ColaboradorDAO e CargoDAO), devemos implementar a classe que acessa o banco de dados Oracle e outro para o SQL. Assim, teremos as classes OracleColaboradorDAO e SQLColaboradorDAO para a interface ColaboradorDAO, OracleCargoDAO e SQLCargoDAO para a interface CargoDAO.
- agora, precisamos desenvolver o AbstractDAOFactory que será responsável por fornecer a instânciada fábrica de DAO, de acordo com o banco escolhido:

~~~java
package br.com.fiap.factory;
  
  import br.com.fiap.dao.CargoDAO;
  import br.com.fiap.dao.ColaboradorDAO;
  
  public abstract class DAOFactory {
  
    //Constanstes que definem os tipos de Data Source suportados
    public static final int SQL_SERVER = 1;
    public static final int ORACLE = 2;
    
    //Atributos que armazenam as instancias de cada Fábrica
    private static DAOFactory oracleDAOFactory;
    private static DAOFactory sqlDAOFactory;
    
    //Método que retorna a instancia de uma fábrica de acordo com o banco
    public static DAOFactory getDAOFactory(int banco){
      switch (banco) {
      case SQL_SERVER:
        if (sqlDAOFactory == null)
          sqlDAOFactory = new SQLDAOFactory();
        return sqlDAOFactory;
      case ORACLE:
        if (oracleDAOFactory == null)
          oracleDAOFactory = new OracleDAOFactory();
        return oracleDAOFactory;
      default:
        return null;
      }
    }
    
    //Assinaturas de métodos que retornam a instancia do DAO
    public abstract CargoDAO getCargoDAO();
    public abstract ColaboradorDAO getColaboradorDAO();
    
  }
~~~

- foram definidas duas constantes, uma para cada banco de dados suportado pela aplicação. 
- o método getDAOFactory() recebe o valor de uma das constantes que representam o banco de dados para devolver a instância da fábrica correta.
- após a criação da classe abstrata, é preciso criar duas classes para estender a DAO Factory, uma para cada tipo de fábrica: SQLDAOFactory e OracleDAOFactory. 
- nessas classes, implementamos os métodos que retornam as instâncias dos DAOs, de acordo com seu banco de dados.
- para utilizar o DAO Factory, basta invocar o método que recupera a instância da fábrica, informando o banco de dados escolhido. 

~~~java
package br.com.fiap.teste;
  
  import java.util.List;
  
  import br.com.fiap.bean.Colaborador;
  import br.com.fiap.dao.ColaboradorDAO;
  import br.com.fiap.factory.DAOFactory;
  
  public class TesteDAOFactory {
  
    public static void main(String[] args) {
      ColaboradorDAO dao = DAOFactory.getDAOFactory(DAOFactory.ORACLE).getColaboradorDAO();
      List<Colaborador> lista = dao.listar();
    }
  }
~~~

## 2.4 Singleton

- objetivo: gerar somente uma instância da classe. 
- esse padrão oferece um ponto de acesso global, no qual todos podem acessar a instância da classe por meio desse ponto de acesso.
- a classe Singleton ndeve gerenciar a própria instância e evitar que qualquer outra classe crie uma instância dela.
- a Singleton deve possuir um construtor privado (private) a fim de evitar que outras classes a instanciem. 
- também deve possuir um método estático que devolve a instância da própria classe Singleton. 
- esse método deve validar se já existe uma instância da classe. Caso não exista, ela deve criar uma nova; caso contrário, deve retornar à instância existente. Para determinar se existe ou não a instância da classe, é preciso criar um atributo estático para armazená-la.

~~~java
package br.com.fiap.singleton;
  
  import java.sql.Connection;
  
  public class ConnectionManager {
  
    //Atributo que armazena a única instancia de ConnectionManager
    private static ConnectionManager instance;
    
    //Construtor privado
    private ConnectionManager(){}
    
    public static ConnectionManager getInstance(){
      if (instance == null){
        instance = new ConnectionManager();
      }
      return instance;
    }
    
    public Connection getConnection(){
      //Implementação
    }
  }
~~~

- a classe ConnectionManager possui uma variável privada e estática que referencia a si mesma, e esse atributo que armazenará a única instância da classe ConnectionManager.
- o construtor possui o modificador de acesso private e, dessa forma, nenhuma outra classe tem acesso ao construtor, não permitindo a sua instanciação.
- para acessar a instância da classe ConnectionManager,é preciso utilizar o método getInstance(), que gerencia a existência da única instância de ConnectionManager, valida se o atributo instance está vazio e, caso esteja, é criada a instância de ConnectionManager,atribuída à variável instance, retornado em seguida. Caso o atributo instance já possua um objeto, o método retorna o próprio objeto existente
- para utilizar a classe ConnectionManager, utilizar o método getInstance():

~~~java
public class OracleColaboradorDAO implements ColaboradorDAO {
    
      public List<Colaborador> listar(){
        Connection conexao = ConnectionManager.getInstance().getConnection();
        //Implementação
      }
      
      public void cadastrar(Colaborador colaborador){
        Connection conexao = ConnectionManager.getInstance().getConnection();
        //Implementação
      }
      
    }
~~~

---

## FAST TEST

### 1. Por meio de um Statement em Java, é possível executar o método executeQuery(). A execução deste método irá retornar uma instância de qual classe?
> ResultSet, responsável pelo conjunto de registros retornados.

### 2. Bancos de dados transacionais, uma vez utilizando essa funcionalidade de consistência, fornecem métodos específicos relacionados a esse tipo de operação. Entre os mais comuns, estão o COMMIT e o ROLLBACK. Qual alternativa representa, respectivamente, o conceito destas duas operações?
> Efetiva as operações da transação em vigor. Não efetiva as operações da transação em vigor.

### 3. Uma instância da classe CallableStatement possui uma grande diferença de utilização para o uso comum da classe PreparedStatement. Qual é essa diferença?
> A CallableStatement é de uso exclusivo para invocação de Stored Procedures e Functions.

### 4. Uma DESIGN PATTERN amplamente utilizada em muitas linguagens modernas de programação são as Singletons. Qual das alternativas define o conceito e uso de uma Singleton?
> Uma Singleton é responsável por ser a representante única como uma instância ativa de sua classe em toda a execução do script ou aplicação.

### 5. Transações garantem consistência quando realizamos operações de gravação e leitura dentro de uma base de dados. Isso também pode ocorrer quando desenvolvemos utilizando o Java. Com esse conceito em mente, ao que remete a sigla ACID?
> Atomicidade, consistência, isolamento e durabilidade.

### 6. Quando utilizamos conexões com banco de dados no ambiente Java, é comum termos contato com diferentes tipos de classes Statement, cada qual com sua particularidade. Qual das alternativas representa alguns tipos de objetos Statement?
> Statement, Prepared Statement e Callable Statement.

### 7. O conceito de DAOs (Data Access Objects) não é exclusivo da linguagem Java, mas, sim, uma DESIGN PATTERN muito utilizada nesse meio. Das alternativas, qual representa a verdadeira vantagem deste padrão de codificação?
> Abstraem e separam a lógica de acesso à manipulação de dados da aplicação.

### 8. Dos diferentes tipos de Statements, qual é a vantagem em utilizar um PreparedStatement?
> A classe PreparedStatement possibilita que sejam passados parâmetros para o comando SQL de forma performática.

---

## Tarefa Cap 8 - Quando o café javanês consulta o oráculo: Exibir e cadastrar informações de uma listagem do Fintech, agora com banco de dados!

<p><em>
"Muito bem, você acaba de saber como o Java faz para acessar o banco de dados Oracle. Vamos aplicar, imediatamente, esse conhecimento tão importante, afinal, seus sistemas computacionais acabam de ganhar um novo grau de complexidade.
<br>
Pré-requisitos técnicos:

- Linguagem de Programação: utilize na Java 17 (IDE Eclipse).
- Banco de dados: utilize Oracle.
- Modelagem do banco de dados: baseie-se na modelagem previamente criada.
- Manipulação de tipos de dados no Java: familiarize-se com a manipulação de dados em Java.

No Capítulo 2 desta mesma Fase, você pode aprender como lidar com vários dados em Java, manipulando listas de objetos.
<br>
Agora vamos dar o próximo passo: faça a classe DAO que você criou acessar o banco de dados, de fato. Crie um método getAll() que deve acessar o banco de dados, realizar um SELECT e receber a consulta, armazenando em uma coleção de dados como vimos no capítulo 2.
<br>
Como os vários passos do acesso ao banco de dados podem ter problemas, tais como o banco estar fora do ar, a tabela ter sido apagada, entre outros, é indispensável realizar o tratamento de exceções.
<br>
Crie também um método insert() na classe do tipo DAO que realize um INSERT e registre uma nova informação. Como você precisa testar o getAll() solicitado acima, utilize seu comando insert() para cadastrar pelo menos cinco novos registros. Use a própria classe Teste, método main(), para inserir os registros e chamar a consulta.
<br>
Requisitos do sistema:

- Classe DAO: Criar a classe DAO responsável por acessar o banco de dados Oracle para a continuação do sistema FINTECH.
- Consulta de dados: Implementar o método getAll na classe DAO. Este método deverá recuperar todos os dados no banco através de um comando SELECT.
- Tratamento de Exceções: Implementar tratamento de exceções para lidar com possíveis problemas durante o acesso ao banco de dados, como indisponibilidade do banco ou tabela inexistente.
- Cadastrar dados: Adicionar o método insert na classe DAO que permita registrar informações no banco de dados.

Instruções para testes:

- Teste de cadastro: Utilizar o método insert para cadastrar pelo menos 5 (cinco) novos registros no banco de dados.
- Teste de consulta: Testar o método getAll após a inserção dos registros, garantindo que ele recupere e apresente corretamente as informações recuperadas.
- Adaptação para Outras Entidades: Replicar o desenvolvimento feito até agora para outras entidades do sistema, com exceção da entidade Usuário. Isso ajudará a avançar na Fase Final do projeto.

Fez com uma entidade? Faça com as demais, exceto Usuário. Assim, você alivia um pouco o número de atividades da Fase Final (na qual você terá muito a fazer!). Depois que a interação com o banco de dados de uma entidade funcionar, ficará mais fácil fazer as demais."
</p></em>

--- 

[Voltar ao início!](https://github.com/DigouO/Fintech_FIAP_2023)