<div id="fase06" align="center">
<h1>FASE 6 - MODEL</h1>
<h2>Capítulo 05: Exceções à regra.</h2>
</div>

<div align="center">
<h2>1. EXCEÇÕES À REGRA</h2>
</div>

## 1.1 Introdução 

- capítulo dedicado a conceitos avançados de orientação a objetos e sua aplicabilidade em Java (possibilidade do polimorfismo, classes abstratas e o uso de exceções para tratar as falhas às quais todo software está sujeito).

## 1.2 Tratamento de exceções

- durante a execução de um programa, é possível que algumas exceções ou erros aconteçam.
- alguns dos problemas mais comuns: 
  - falha na aquisição de algum recurso, como abrir um arquivo, conectar com o banco de dados ou acessar um web service.
  - tentativa de realizar algo impossível, como a divisão de um número por zero, acessar uma posição que não existe em um array.
  - outras condições inválidas, como evocar um método de um objeto que não foi instanciado ou realizar um cast inválido.
- esses eventos não esperados geralmente interrompem o fluxo da execução do código.
- o tratamento de exceções permite verificar esses eventos (erros) e realizar uma ação sem prejudicar o fluxo do programa.
- em geral, o fluxo para o tratamento de exceções no Java ocorre em `três passos`:
  - ***uma exceção é lançada***: um comando do código dispara uma condição inesperada de erro.
  - ***a exceção é capturada***: em algum ponto do código, podemos adicionar um comando para capturar a possível exceção.
  - ***o tratamento de erro é realizado***: após a captura da exceção, o tratamento de erro adequado é executado.

> IMPORTANTE: Realizando o tratamento das exceções, o programa consegue continuar a execução normalmente. Exceções não capturadas provocam a finalização do programa.

## 1.3 Classificação

- uma exceção é um objeto do tipo Exception.
- no polimorfismo, um objeto desse tipo pode ser qualquer instância de uma subclasse de Exception.
- dentro da plataforma Java, podemos classificar as exceções em:
  - `Checked`: exceção que deve ser tratada ou relançada pelo desenvolvedor, geralmente herda da classe Exception. 
  - `Unchecked`: exceção que pode ser tratada ou relançada pelo programador. Essa exceção é gerada pelo código mal escrito. Caso a exceção não seja tratada, ela será automaticamente relançada. Geralmente, esse tipo de exceção herda de RuntimeException.
  - `Error`: erro crítico, utilizado pela JVM para indicar que existe um problema que não permite a continuação da execução do programa.

<div align="center">

Classe | Objetivo | Erro
-------|----------|--------------
Error | Erro que não pode ser tratado na aplicação. Lançado pela JVM indicando que o programa não pode continuar a execução. | OutOfMemoryError: indica que não há memória suficiente na máquina para continuar a execução do programa.
Exception | Exceção que deve ser tratada pelo desenvolvedor. | ArithmeticException: indica que houve alguma operação aritmética inválida, exemplo: divisão por zero.
RuntimeException | Exceção que pode ser tratada pelo desenvolvedor. | NullpointerException: indica que há uma tentativa de acessar algum método ou atributo de uma classe que não foi instanciada.

</div>

- além das exceções existentes na plataforma, podemos criar as nossas próprias exceções, sejam elas checked (filhas de exception) ou unchecked(filhas de RuntimeException).
- hierarquia de classes de exceções do Java:

<div align="center">
<img src="./assets/hierarquia-excecoes.png" width="50%"/><br/>
</div>

- a classe Throwable tem duas subclasses: Exception e Error
  - Exception é a classe base para as subclasses de exceções checked e unchecked, exceções que devem ou podem ser tratadas. 
  - Error é a base para as classes de exceções que não podem ser tratadas.
- `exceções mais comuns em Java`:

1. ***ArithmeticException***:

- exceção unchecked.
- ocorre quando alguma operação aritmética é inválida; operação esta que não pode ser resolvida, como é o caso da divisão de um número por zero.

2. ***ArrayIndexOutOfBoundsException***:

- exceção do tipo unchecked (o desenvolvedor não é obrigado a tratar a exceção).
- acontece quando tentamos acessar uma posição inválida de uma matriz ou vetor (array). 
  - uma posição inválida é uma posição que não existe (negativa ou valor igual ou maior que o tamanho do vetor). 
  - lembre-se: o índice do vetor sempre começa em zero, ou seja, não existe posição negativa e o último elemento de um array está posicionado no tamanho do vetor menos um.

3. ***NullpointerException***:

- é uma exceção unchecked, mais conhecida e comum durante o desenvolvimento.
- ocorre na tentativa de acessar um objeto que ainda não foi instanciado.
- exemplo: quando tentamos acessar o método size() de um ArrayList que ainda não foi instanciado. 

4. ***FileNotFoundException***:

- exceção checked.
- precisamos tratar quando tentamos acessar um arquivo que não foi encontrado.

5. ***NumberFormatException***:

- não precisa ser tratada (unchecked).
- ocorre quando tentamos transformar uma string inválida em algum tipo numérico. 

## 1.4 Captura e tratamento de exceções

- para tratar as exceções (checked ou unchecked) em tempo de execução, elas devem ser capturadas e tratadas. 
- o Java possui duas estruturas importantes para o tratamento de exceções: `try-catch` e `try-catch-finally`.
- essas estruturas têm a finalidade de separar o código que executa as tarefas desejadas das rotinas de tratamento das exceções.

~~~java
try {
  //Código
} catch(Excecao) {
  //Tratamento da exceção
}
~~~

- o `bloco try` tem um código que pode gerar uma exceção, ou seja, esse trecho de código será monitorado pela JVM. 
  - se um erro for gerado, o fluxo da execução será desviado para o bloco catch, para o tratamento do erro.
  - o uso do try indica que o código está tentando realizar algo “perigoso”, passível de erro. 
- o `bloco catch` só é executado se uma exceção for gerada. 
  - caso nenhuma exceção seja lançada, a execução pula o bloco catch e continua normalmente. 
  - se uma exceção for lançada, o bloco try é finalizado e o fluxo de execução procura por um bloco catch adequado para tratar a exceção.
  - depois de executar o bloco catch, a execução do programa continua na primeira instrução após o último bloco catch.
  - podemos adicionar vários blocos catch para capturar diferentes tipos de exceções:

~~~java
try {
  // Código
  } catch (Excecao1) {
    // Tratamento da exceção 1
  } catch (Excecao2) {
    //Tratamento da exceção 2
  } catch (Excecao3) {
    //Tratamento da exceção 3
}
~~~

- os catches são testados de cima para baixo, um por um, até que o catch apropriado seja executado, por isso as exceções mais específicas devem ser colocadas nos primeiros catches, sempre obedecendo à ordem das exceções mais específicas para as mais genéricas.
- a `exceção Exception` é a mais genérica possível, pois todas as exceções (checked ou unchecked) são filhas dela. 
  - portanto, a captura dessa exceção deve ser colocada no último catch, pois ela captura qualquer tipo de exceção que for lançada.
  - se nenhum catch conseguir capturar a exceção lançada, ela não será tratada, como se não existisse o bloco try-catch.
  - exemplo:

~~~java
Scanner sc= new Scanner(System.in);
//Lê os dois números
int numero1 = sc.nextInt();
int numero2 = sc.nextInt();
//Realiza a divisão
int divisao = numero1/numero2;
//Exibe o resultado
System.out.println("O resultado é: "+ divisao);
sc.close();
~~~

- código é simples, porém pode lançar uma exceção, caso o segundo número informado pelo usuário seja zero; caso isso aconteça, o erro gerado será:

~~~
2
0
Exception in thread "main" java.lang.ArithmeticException: / by zero
at br.com.fiap.tds.View.main(View.java:16)
~~~

- a `exceção ArithmeticException` foi lançada, pois não é possível realizar uma divisão por zero! 
- essa exceção é unchecked, já que não fomos obrigados a tratá-la.
- realizando alteração no código, para realizar o tratamento da exceção:

~~~java
Scanner sc = new Scanner(System.in);
// Lê os dois números
int numero1 = sc.nextInt();
int numero2 = sc.nextInt();

try {
  // Realiza a divisão
  int divisao = numero1 / numero2;
  // Exibe o resultado
System.out.println("O resultado é: "+ divisao);
} catch(ArithmeticException e) {
  System.err.println("Erro ao dividir por zero!");
}
sc.close();
~~~

- neste caso, o bloco try-catch captura a exceção: caso o usuário insira um divisor igual a zero, a divisão vai gerar a ArithmeticException. 
- assim, o fluxo da execução será desviado para o bloco catch, e a linha do código que exibe o resultado não será executada; o tratamento de exceção previsto no catch para o erro consiste na apresentação da mensagem Erro ao dividir por zero, retornando:

~~~
2
0
Erro ao dividirpor zero!
~~~

- se o programa rodar sem lançar exceção (se o usuário informar o dividendo diferente de zero), o resultado da divisão será exibido e o bloco catch não será executado.
- dentro do bloco catch, podemos recuperar a exceção gerada, por meio do parâmetro; `no exemplo dado, a exceção é recuperada no parâmetro com o nome "e"`.
- A `classe Throwable` possui alguns métodos que podem exibir informações dos erros gerados, então, por herança, a exceção ArithmeticException também tem estes métodos:
  - ***printStackTrace()***:
    - imprime a pilha de erro encontrada na exceção.
    - nesta pilha, podemos verificar o número da linha e a classe na quala exceção foi gerada.
  - ***getMessage()***:
    - retorna uma mensagem contendo a lista de erros armazenados em uma exceção.
- resultado retornado pelo método printStackTrace e a mensagem de erro da exceção:

~~~java
int[] array = new int[2];
try {
  //Tentaa cessar uma posição inexistente do vetor 
  array[2] = 10;
} catch (ArrayIndexOutOfBoundsException e) {
  System.err.println("Mensagem de erro: "+ e.getMessage());
  e.printStackTrace();
}
~~~

- a exceção é gerada quando tentamos acessar uma posição inválida de um array: ArrayIndexOutOfBoundsException.
- no bloco catch, utilizamos os métodos getMessage() e printStackTrace(), resultando em:

~~~
Mensagem de erro: 2
java.lang.ArrayIndexOutOfBoundsException: 2
at br.com.fiap.tds.View.main(View.java:10)
~~~

- a mensagem tem o valor do índice inválido que tentamos acessar no array. 
- o método printStackTrace imprime o rastro da pilha e exibe a exceção, a classe e a linha que gerou a exceção: View.java:10. Classe View, linha 10.
- utilizamos o `System.err` para exibir a mensagem de erro:
  - é uma classe utilizada para exibir os erros em um programa Java.
  - podemos enviar o fluxo de saída para um arquivo de log, enquanto o fluxo de saída padrão de um System.out é a tela da aplicação.
  - além do try-catch, podemos utilizar o bloco try-catch-finally para tratar as exceções.
  - o terceiro bloco finally é opcional e utilizado sempre que precisamos executar um código, independentemente de ter ou não acontecido uma exceção.
    - se uma exceção for lançada: o fluxo de execução passa do bloco try para o bloco catch adequado e, após a sua execução, o bloco finally será processado.
    - se não for gerado uma exceção: após executar todo o bloco try, o bloco finally será processado.
  - exemplo:

~~~java
try {
  //Fluxo normal que pode gerar uma exceção
} catch (Exception e) {
  //Fluxo alternativo, para tratamento da exceção
} finally {
  //Fluxo normal, que sempre será executado
}
~~~

- um exemplo clássico da utilização do bloco finally é o fechamento da conexão com o banco de dados (sempre devemos fechar a conexão, independentemente da concretização ou não da operação no banco).
- voltando ao primeiro exemplo, vamos tratar as exceções de divisão por zero e entrada de dados inválida, quando o usuário digita um número inválido; também vamos adicionar um bloco finally para exibir uma mensagem para o usuário e fechar o objeto scanner:

~~~java
Scanner sc = new Scanner(System.in);
try {
  // Lê os dois números
  int numero1 = sc.nextInt();
  int numero2 = sc.nextInt();
  // Realiza a divisão
  int divisao = numero1 / numero2;
  // Exibe o resultado
  System.out.println("O resultado é: "+ divisao);
} catch (ArithmeticException e) {
  System.err.println("Erro ao dividir por zero!");
} catch (InputMismatchException e) {
  System.err.println("Erro de entrada de dados!");
} finally {
  System.out.println("Finalizando a execução do programa!");
  sc.close();
}
~~~

- portanto, há 3 possíveis fluxos de execução:

1. Sem gerar exceção, a saída será: 

~~~
2
2
O resultado é: 1
Finalizando a execução do programa!
~~~

2. Em exceção causada pela divisão por zero, a saída será:

~~~
2
0
Erro ao dividir por zero!
Finalizando a execução do programa!
~~~

3. Em exceção causada pelo valor inserido inválido, a saída será:

~~~
a
Erro de entrada de dados!
Finalizando a execução do programa!
~~~

> Observe que todos os fluxos sempre executam o bloco finally!

## 1.5 Propagação de exceções – Throws

- umm método pode optar por não tratar a exceção e simplesmente propagá-la, ou melhor, delegá-la para o método que a chamou.
- podemos notificar o método que invocou outro método em que alguma exceção ocorreu.
- exemplo: criar uma classe chamada Calculadora que será responsável por implementar as operações aritméticas, entre eles a divisão.

~~~java
public class Calculadora {
  public int dividir (int n1, int n2) {
    return n1/n2;
  }
}
~~~

- esse método pode lançar uma exceção, caso o valor de n2 seja zero. 
- podemos utilizar o try-catch para tratar a exceção, porém quem chamar o método dividir não saberá se a operação ocorreu de forma correta ou se aconteceu algum erro.

~~~java
public int dividir (int n1, int n2) {
  try {
    return n1/ n2;
  } catch (ArithmeticException e) {
    e.printStackTrace();
  }
  return 0;
}
~~~

- nesse exemplo, quando o método dividir for acionado e o usuário informar para n2 o valor zero, internamente, no método dividir, será feito o tratamento do erro e ele retornará para o ambiente de chamada o valor zero e, nesse caso, o usuário não será informado sobre a ocorrência do erro!!!
- logo, ***a melhor maneira de tratar a exceção é não a tratar***; no caso, somente propagar a exceção, notificando ao ambiente de chamada que algum problema aconteceu na execução: adicionar na assinatura do método o throws, com a exceção que queremos propagar!

~~~java
public int dividir (int n1, int n2) throws Exception {
  return n1 / n2;
}
~~~

- um método pode propagar mais de um tipo de exceção.
- para isso, adicionar as exceções separadas por vírgula.

~~~java
public void gravarArquivo (String valor) throws SecurityException, FileNotFoundException, IOException {
  //Código...
}
~~~

- portanto, ***a cláusula throws declara exceções que podem ser lançadas em determinados métodos***.
- é uma vantagem para os devs, pois deixamos de modo explícito os eventuais erros que podem ocorrer na chamada do método, permitindo que o tratamento adequado para o erro seja implementado.
- podemos também lançar uma nova exceção nesse método, utilizando o comando throw:

~~~java
public void depositar (double valor) {
  if (valor < 0) {
    throw newIllegalArgumentException();
  } 
  saldo = saldo + valor;
}
~~~

- no exemplo, estamos validando se o valor depositado é maior do que zero. 
  - em caso positivo, o valor é adicionado ao saldo.
  - caso contrário, uma exceção do tipo IllegalArgumentException será lançada, o que indica que o valor passado como parâmetro para o método é inválido.
- não foi preciso adicionar o throws na assinatura do método, pois essa exceção é unchecked. Caso a exceção seja checked, é necessário declará-la na assinatura do método!

~~~java
public void sacar (double valor) throws Exception {
  if (valor > saldo) {
    throw new Exception ("Saldo insuficiente");
  }
  saldo = saldo - valor;
}
~~~

- o método acima valida se o valor a ser retirado é maior do que o valor do saldo. 
- caso o valor do saldo seja insuficiente, uma exceção será lançada (foi necessário adicionar o throws na assinatura do método, para que, quem chamar o método sacar possa tratar a exceção ou lançá-la novamente).

~~~java
public static void main (String[] args) {
  // Cria uma nova instância de Conta
  Conta c = new Conta();
  try {
    // Saca
    c.sacar(100);
  } catch (Exception e) {
    e.printStackTrace();
  }
  // Deposita
  c.depositar(200);
}
~~~

- após criar um novo objeto conta, chamamos o método sacar e, como lança uma exceção checked, precisamos tratá-la ou lançá-la.
  - nesse caso, optamos por tratar a exceção com o bloco try-catch.
- já o método depositar lança uma exceção unchecked, não sendo obrigados a tratá-la. 
  - porém, se uma exceção ocorrer, ela será relançada automaticamente pelo método main, que imprimirá o erro no console!

## 1.6 Criação de exceções

- é possível também criar as nossas próprias classes de exceções. 
- exemplo "Método sacar":
  - lança a exceção mais genérica possível (Exception). 
  - para melhorar o uso das exceções e não utilizar uma exceção que serve para tudo, podemos criar uma exceção específica para o erro que pode acontecer.
- para criar uma exceção, criar uma classe que herde de Exception(checked) ou RuntimeException (unchecked).
- vamos criar nossas exceções: uma para identificar que o valor de saque é inválido e outra para dizer que o saldo da conta é insuficiente.
  - a primeira exceção será unchecked (vai descender de RuntimeException). Por padrão, as exceções no Java terminam com Exception.

~~~java
public class ValorInvalidoException extends RuntimeException {
  // ...
}
~~~

- para utilizá-la, modificar o método sacar para que lance a exceção customizada:

~~~java
public void depositar (double valor) {
  if (valor < 0) {
    throw new ValorInvalidoException();
  }
  saldo = saldo + valor;
}
~~~

- agora vamos criar uma exceção checked que verifique se o saldo é insuficiente:

~~~java
public class SaldoInsuficienteException extends Exception{
  // ...
}
~~~

- para utilizá-la, podemos relançá-la, não nos esquecendo de modificar o throws na assinatura do método:

~~~java
public void sacar (double valor) throws SaldoInsuficienteException {
  if (valor > saldo) {
    throw new SaldoInsuficienteException();
  }
  saldo = saldo - valor;
}
~~~

- nos exemplos anteriores, criamos exceções checked e unchecked para ilustrar nossos exemplos, mas nada impede de elaborar somente um tipo de exceção para a classe Conta. 
- ***procure sempre utilizar as exceções customizadas com informações do motivo do erro!***

## 1.7 Acesso a arquivos

- o armazenamento de dados em variáveis, arrays, coleções ou outra estrutura de dados em memória é temporário (são perdidas quando o programa termina).
- os arquivos são utilizados para persistência de dados (armazenamento mesmo após o término da execução do programa).
- para armazenar grandes quantidades de informações, como clientes, produtos ou vendas de uma empresa, os lugares mais adequados são os bancos de dados.
- vantagens dos arquivos:
  - úteis para armazenar as configurações do programa, ao invés de colocar as configurações diretamente no código-fonte. 
  - possibilidade de alterar o arquivo de configurações sem a necessidade de recompilar e empacotar todo o programa novamente.
  - integração de sistemas diferentes (um sistema pode realizar um processamento de informações e gerar um arquivo final, enquanto outro sistema pode ler esse arquivo e apresentar as informações, gerando a integração). 
- a plataforma Java possui facilidade na leitura e gravação de arquivos, pois é independente de plataforma, logo não precisamos nos preocupar com o tipo de sistema operacional em que o programa será executado.
- todas entradas e saídas em Java são definidas em termos de `fluxos`, ou `streams`: sequências ordenadas de dados que possuem uma fonte de origem (streams de entrada), ou um destino (streams de saída).
  - uma stream é uma conexão para uma fonte de dados ou para um destino de dados. 
  - a plataforma Java trata cada arquivo como uma stream!
- há `dois tipos de streams`, dependendo da operação que será realizada:
  - ***Output stream***: para gravar em um destino.
  - ***Input stream***: para ler de uma fonte.
- arquivos baseados em um fluxo de caracteres são chamados `arquivos textos`:
  - pode ser lido e entendido pelas pessoas, e também manipulado na plataforma Java. 
  - geralmente, registros contidos neles são representados pelas linhas, enquanto os campos o são por colunas ou valores separados por vírgula.
  - para ***gravar dados em um arquivo texto***, é preciso executar três passos: abrir o arquivo > gravar os dados > fechar o arquivo.
  - as ***classes para manipular os arquivos*** ficam dentro do pacote java.io:
    - ***java.io.FileWriter*** e 
    - ***java.io.PrintWriter***.

### Aplicando:

1. `classe FileWriter`:
  - filha da classe OutputStreamWriter.
  - utilizar essa classe para abrir o arquivo para escrita.

2. `classe PrintWriter`:
  - usada para escrever no arquivo. 
  - para criar um objeto do tipo PrintWriter, é preciso passar o arquivo, ou seja, o objeto FileWriter.

~~~java
public static void main(String[] args) {
  try {
    //Abre o arquivo 
    FileWriter stream = new FileWriter("arquivo.txt");
    PrintWriter print = new PrintWriter (stream);
    //Escreve no arquivo
    print.println("Teste");
    print.println("Escrevendo no arquivo");
    print.close();
    //Fecha o arquivo
    stream.close();
  } catch (IOException e) {
    e.printStackTrace();
  }
}
~~~

- o exemplo acima apresenta o método main, que abre, escreve e fecha o "arquivo.txt" (aberto, se existir, ou criado, caso não exista). 
- na instanciação do FileWriter, é passado o caminho e nome do arquivo. Como não especificamos nenhum caminho, o arquivo estará na pasta raiz do programa.
  - podemos também especificar o caminho completo do arquivo:

~~~java
FileWriter stream = new FileWriter("C://arquivo.txt");
~~~

- após criar o objeto FileWriter, instanciado o objeto PrintWriter, passando como parâmetro o objeto que encapsula o arquivo:

~~~java
PrintWriter print = new PrintWriter(stream);
~~~

- com o objeto PrintWriter, é possível utilizar os métodos print ou println para escrever no arquivo:

~~~java
print.println("Teste");
print.println("Escrevendo no arquivo");
~~~

- para finalizar, chamamos o método close do objeto PrintWriter e FileWriter, fechando o arquivo texto:

~~~java
print.close();
stream.close();
~~~

- foi preciso tratar a exceção IOException, pois podemos ter problemas na hora de abrir ou manipular o arquivo.
- o resultado da execução será o arquivo texto com as informações gravadas.

### Lendo o arquivo:

- para ler o arquivo, três passos: abrir o arquivo > utilizar o arquivo (ler os dados) > fechar o arquivo.
- `classes que podemos utilizar`:
  - ***java.io.FileReader*** (descende da classe InputStreamReader) e 
  - ***java.io.BufferedReader***.
- exemplo:

~~~java
public static void main(String[] args) {
  try {
    //Abre o arquivo
    FileReader stream = new FileReader("arquivo.txt");
    BufferedReader reader = new BufferedReader(stream);
    //Lê uma linha do arquivo
    String linha = reader.readLine();
    while (linha != null) {
      System.out.println(linha);
      //Lê a próxima linha do arquivo
      linha = reader.readLine();
    }
    reader.close();
    //Fecha o arquivo
    stream.close();
  } catch (IOException e) {
    e.printStackTrace();
  }
}
~~~

- a mesma regra do caminho se aplica: caso o arquivo esteja em outro diretório, devemos especificá-lo:

~~~java
FileReader stream= new FileReader("C://arquivo.txt");
~~~

- para finalizar, é preciso fechar o FileReader e o BufferedReader.
- a plataforma Java oferece várias Classes para leitura/escrita de arquivos textos.

<div align="center">
<img src="./assets/hierarquia-pacote-javaio.svg" width="60%"><br>
<p><em>Hierarquia do pacote java.io.</p></em>
</div>

- as principais classes desse pacote são:

1. ***Classes para entrada ou saída baseada em bytes***:
  - FileInputStream: para entrada baseada em bytes de um arquivo.
  - FileOutputStream: para saída baseada em bytes para um arquivo.
  - RandomAccessFile: para entrada e saída baseada em bytes de e para um arquivo.

2. ***Classes para entrada e saída baseada em caracteres***:
  - FileReader: para entrada baseada em caracteres de um arquivo.
  - FileWriter: para saída baseada em caracteres para um arquivo.

- ***outra classe importante da API de entrada e saída (IO) do Java é o `File`***:
  - representa um arquivo ou um diretório no sistema de arquivo nativo. 
  - permite obter informações sobre o arquivo ou diretório, e não sobre o seu conteúdo (não abre o arquivo ou permite processamento de conteúdo).
  - sua função é gerenciar o arquivo ou diretório, o seu caminho (path), verificar permissões, existência, criar, renomear etc.
  - um objeto da classe File representa o arquivo/diretório, não quer dizer que o arquivo ou diretório exista de fato.
  - principais métodos da classe File:

<div align="center">

Método | Descrição
-------|--------------
exists | Verifica se um arquivo ou diretório existe
isDirectory | Verifica se é um diretório
isFile | Verifica se é um arquivo
canRead | Verifica se pode ser lido
canWrite | Verifica se pode ser gravado
mkdir | Cria um diretório
renameTo | Renomeia um arquivo ou diretório
length | Retorna o tamanho do arquivo
delete | Deleta um arquivo ou diretório
getPath | Retorna o caminho

</div>

~~~java
public static void main(String[] args) {
  File arquivo = new File("arquivo.txt");
  // Verifica se o arquivo existe
  if (arquivo.exists()) {
    System.out.println("O arquivo existe!"+
      "\nPode ser lido: "+ arquivo.canRead() +
      "\nPodeser gravado: "+ arquivo.canWrite() +
      "\nTamanho: "+ arquivo.length() +
      "\nCaminho: "+ arquivo.getPath());
  } else {
    // Cria o arquivo
    try {
      if(arquivo.createNewFile())
        System.out.println("Arquivo criado!");
      else
        System.out.println("Arquivo não criado!");
    } catch (IOException e) {
        e.printStackTrace();
    }
  }
}
~~~

- podemos também utilizar o objeto File para verificar se um diretório  existe, ou então para criá-lo:

~~~java
public static void main(String[] args) {
  File diretorio = new File("fiap");
  if(diretorio.exists()) {
    System.out.println("Diretório existe!");
  } else {
    if(diretorio.mkdir())
      System.out.println("Diretório criado!");
    else
      System.out.println("Diretório não criado.");
  }
}
~~~

- após criar um diretório, podemos criar um arquivo dentro dele, conforme:

~~~java
public static void main(String[] args) {
  File diretorio = new File("fiap");
  if (diretorio.exists()) {
    System.out.println("Diretório existe!");
  } else {
    if (diretorio.mkdir())
      System.out.println("Diretório criado!");
    else
      System.out.println("Diretório não criado.");
  }
  File arquivo = new File (diretorio,"file.txt");
  try {
    if(arquivo.createNewFile())
      System.out.println("Arquivo criado!");
    else
      System.out.println("Arquivo não criado!");
  } catch(IOException e) {
    e.printStackTrace();
  }
}
~~~

- primeiro verificamos se o diretório existe e, caso necessário, o criamos. Depois, instanciamos uma classe File passando o nome do arquivo e o objeto File que representa o diretório.
- com esse novo objeto File, tentamos criar o arquivo dentro do diretório.
- a classe File pode ser utilizada em conjunto com as outras classes de manipulação do conteúdo do arquivo, basta utilizar o objeto File no momento de criar um FileWriter ou FileReader:

~~~java
try {
  //Abre o arquivo para escrita
  FileWriter writer = new FileWriter(arquivo);
  //Abre o arquivo para leitura
  FileReader reader = new FileReader(arquivo);
  //Código...
} catch(IOException e) {
  e.printStackTrace();
}
~~~

- depois, basta instanciar a classe PrintWriter para escrever no arquivo ou um BufferedReader para ler.

## 1.8 Polimorfismo

- significa: "qualidade ou estado de ser capaz de assumir diferentes formas".
- na programação orientada a objetos, polimorfismo significa ter múltiplos comportamentos. 
- um método polimórfico resulta em diferentes ações, dependendo do objeto que está sendo referenciado.
- a capacidade polimórfica decorre diretamente da herança, pois permite que uma variável de referência e o objeto sejam diferentes.
- exemplo:
  - podemos definir uma variável do tipo Conta, e armazenar um objeto de ContaCorrente, se este herdar da classe Conta.
  - portanto, o tipo da variável de referência pode ser uma superclasse para o tipo do objeto real.
  - qualquer objeto de uma classe que herde o tipo declarado da variável pode ser atribuído a ela!
- ***a utilização mais importante do polimorfismo se dá nas ocasiões em que dois objetos, sendo um da superclasse e outro da subclasse, executam ações diferentes quando o mesmo método é invocado***, o que é possível por meio da `sobrescrita de métodos` (quando a subclasse sobrescreve o método implementado na superclasse).

~~~java
public class Conta { //superclasse conta
  protected double saldo;
  public void sacar(double valor) throws SaldoInsuficienteException {
    if(valor > saldo) {
      throw new SaldoInsuficienteException();
    }
    saldo = saldo - valor;
  }
}

public class ContaCorrente extends Conta { // subclasse cc
  private double limite;
  @Override
  public void sacar(double valor) throws SaldoInsuficienteException {
    if(valor > saldo + limite) {
      throw new SaldoInsuficienteException();
    }
    saldo = saldo-valor;
  }
}

public static void main(String[] args) {
  Conta cc = new ContaCorrente();
  try {
    cc.sacar(20);
  } catch(SaldoInsuficienteException e) {
    e.printStackTrace();
  }
}
// O método do objeto armazenado na variável será executado,
// ou seja, o método definido na ContaCorrente.
~~~

- a execução sempre acontece com o objeto armazenado e não com o tipo da variável!

## 1.9 Classe abstrata

- a classe abstrata possui algumas características:
  - não pode ser instanciada (não podemos utilizar o operador new).
  - pode possuir métodos abstratos.
- o propósito de uma classe abstrata é atuar como uma superclasse (existe para ser herdada, será a base para as outras classes que serão desenvolvidas).
- exemplo: a classe Conta é perfeita para ser abstrata, pois será a base para todas as outras contas em nosso sistema, como contas corrente, poupança, investimento, etc (não instanciamos uma classe Conta, não existe uma "conta genérica").
- uma classe abstrata pode conter métodos abstratos (não possui implementação, define somente a assinatura do método). A sua subclasse, obrigatoriamente, precisará implementar o método, caso esta seja concreta.
- em uma classe concreta, não é permitido definir métodos abstratos.
- é possível ter uma herança com várias classes abstratas, porém a primeira classe concreta da hierarquia será obrigada a implementar todos os métodos abstratos definidos pelas suas superclasses (é igual a sobrescrever, devemos definir um método com o mesmo nome e parâmetros (assinatura) na subclasse e implementá-la). 

~~~java
public abstract class Conta {
	protected double saldo;

	public void sacar(double valor) throws SaldoInsuficienteException {
		if (valor > saldo) {
			throw new SaldoInsuficienteException();
		}
		saldo = saldo - valor;
	}
public abstract double verificarSaldo();
}
~~~

- o nome da classe abstrata e o método abstrato ficam em itálico. 
- as classes concretas e os métodos implementados são exibidos sem nenhuma formatação diferente.
- para definir uma classe ou um método abstrato, adicionar o modificador abstract.
- no exemplo, definir a classe Conta como abstrata e adicionar o método “depositar” como abstrato:

~~~java
public abstract class Conta {
	protected double saldo;

	public void sacar (double valor) throws SaldoInsuficienteException {
		if (valor > saldo){
			throw new SaldoInsuficienteException();
		}
		saldo = saldo - valor;
	}
public abstract double verificarSaldo();
}
~~~

- o método verificarSaldo é abstrato (não há implementação), então a assinatura do método termina com ponto e vírgula (;).
- a subclasse ContaCorrente está com erro de compilação devido à adição do método abstrato na classe Conta; portanto, implementar o método verificarSaldo na classe ContaCorrente:

~~~java
public class ContaCorrente extends Conta{

	private double limite;

	@Override
	public void sacar(double valor) throws SaldoInsuficienteException {
		if (valor > saldo + limite){
			throw new SaldoInsuficienteException();
		}
		saldo = saldo - valor;
	}

	@Override
	public double verificarSaldo() {
		return saldo + limite;
	}

//Gets e Sets
}
~~~
- implementar a classe ContaPoupanca:

~~~java
public class ContaPoupanca extends Conta {
	@Override
	public double verificarSaldo() {
		return saldo;
	}
}
~~~

- a classe ContaPoupanca é obrigada a implementar o método verificarSaldo, pois ela é concreta. 
- porém, ela não foi obrigada a implementar o método sacar, pois esse método não é abstrato e está implementado na superclasse Conta! 
- dessa forma, a classe ContaPoupanca possui o mesmo método sacar da classe Conta e implementa um comportamento específico no método verificarSaldo.

---

<div align="center">
<h2>2. MODIFICADOR FINAL</h2>
</div>

- trabalha de forma contrária em relação ao modificador abstract.
- uma classe Java marcada como final não pode ser estendida.
- exemplo: classe ContaPoupanca não pode possuir nenhuma subclasse.

~~~java
public final class ContaPoupanca extends Conta {
		@Override
		public double verificarSaldo() {
			return saldo;
		}
}
~~~

- além das classes, também podemos utilizar a palavra-chave final em atributos, e seu valor será imutável (ou seja, não podemos alterar o valor do atributo durante o ciclo de vida do objeto).
- atributos declarados como final são chamados de atributos constantes e sua inicialização deve ser feita no momento da declaração!

~~~java
public class Circulo {
		private final double NUMERO_PI = 3.1416;
}
~~~

- por convenção, `atributos constantes` devem ser criados com todas as letras em maiúsculas, e caso o nome seja composto por mais de uma palavra, separa-las pelo caractere underline.

- além de classes e atributos, podemos utilizar o modificador final também `em métodos` (não poderá ser sobrescrito).

~~~java
public final double calcularArea(){
		return NUMERO_PI*raio*raio;
}
~~~

- o modificador final é importante quando queremos que nenhum outro desenvolvedor estenda a nossa classe ou modifique o comportamento de um método em uma classe filha.
- é utilizado também para criar valores constantes.
- principais características da palavra-chave final, dependendo de onde está sendo utilizada:

<div align="center">

Elemento | Comportamento
-----------|------------
Classe | A classe não poderá ser estendida, ou seja, não possuirá subclasses.<br>A classe String, por exemplo, é final. 
Método | O método não poderá ser sobrescrito.
Atributo | O valor do atributo definido na sua declaração não poderá ser alterado.

</div>

## 2.1 Modificador static

- pode ser aplicado aos membros de uma classe: métodos e atributos.
- é compartilhado por todas as instâncias de uma determinada classe. 
- quando um atributo é declarado como estático, ele passa a se referir à Classe e não mais à instância da Classe, ou seja, o atributo será igual para todos os objetos, independentemente dos respectivos números de instâncias.
- por isso, se um objeto mudar o valor do atributo estático, todos os outros objetos terão acesso ao novo valor.
- um método marcado como estático não depende das características de cada objeto. Podem ser invocados sem precisar de uma instância da classe e são utilizados para realizar uma tarefa comum para todos os objetos:

~~~java
public static void main(String[] args) {
  // ...
}
~~~

- um método estático utiliza apenas informações contidas em seus parâmetros e nos atributos estáticos, ou seja, pode acessar somente atributos estáticos. Porém, o contrário é possível: pode-se acessar um atributo estático dentro de um método não estático.

~~~java
public class AcessoCatraca {
	private static int totalAcesso;

	private String nome;

	public void entrar(String nome){
		this.nome = nome;
		totalAcesso = totalAcesso + 1;
	}

	public static int recuperarTotal(){
		return totalAcesso;
	}
}
~~~

- um exemplo de utilização de métodos estáticos é a classe ***java.lang.Math***, que possui vários métodos estáticos que auxiliam o dev nas operações matemáticas.
- para utilizar um método estático não é preciso de uma instância da classe:

~~~java
public static void main(String[] args) {
		int total = AcessoCatraca.recuperarTotal();
		System.out.println("Total " + total);

		long numero = Math.round(2.9);
		System.out.println("Número arredondado: " + numero);
}
~~~

- o exemplo acima acessa o método estático recuperarTotal, da classe AcessoCatraca, e utiliza um método de arredondamento da classe Math.Em ambos os casos, não foi preciso instanciar suas respectivas classes.
- para acessar o método entrar, da classe AcessoCatraca, será preciso criar o objeto:

~~~java
public static void main(String[] args) {
		AcessoCatraca a1 = new AcessoCatraca();
		a1.entrar("Thiago");

		AcessoCatraca a2 = new AcessoCatraca();
		a2.entrar("Leandro");

		int total = AcessoCatraca.recuperarTotal();
		System.out.println("Total " + total);
}
~~~

- Qual será o resultado da execução acima? O método entrar incrementa o valor do atributo estático totalAcesso (um atributo estático se refere à classe e não ao objeto, então compartilharãoo mesmo valor).
- como o método foi chamado duas vezes, independentemente do objeto, no final da execução o valor total será 2.

## 2.2 Constantes

- é comum usar modificadores public, static e final ao declarar uma constante no Java.
- constantes podem ser:
  - públicas (todos podem ter acesso), 
  - estáticas (pois não existe necessidade de cada objeto ter sua própria constante) 
  - e finais (para que o valor da constante nunca se altere).
- por convenção, o nome de uma constante é sempre escrito em maiúsculo, com as palavras separadas por underline.
- para acessar as constantes, utilizar o nome da classe.

~~~java
public class Constantes {
	public static final String JANEIRO = "Janeiro";
	public static final double TAXA_RETIRADA = 10;
	public static final int NUMERO_DIAS_SEMANA = 7;
	public static final Estado SAO_PAULO = new Estado("São Paulo","SP");
}

public static void main(String[] args) {
		System.out.println(Constantes.JANEIRO);
		System.out.println(Constantes.TAXA_RETIRADA);
}
~~~

## 2.3 Interfaces

- uma interface define um conjunto de requisitos para as classes implementá-las. Porém, `interface não é classe`.
- interface é um contato entre a classe e o mundo externo.
- quando uma classe implementa uma interface, está comprometida a fornecer todos os comportamentos definidos na interface.
- uma interface em Java não pode ser instanciada; também pode ser composta de atributos e métodos, porém, como não é instanciada, não apresenta construtores.
- a plataforma Java não permite herança múltipla: não é possível herdar duas classes diretamente. Porém, `uma classe Java pode implementar uma ou mais interfaces`, devendo definir todos os métodos publicados por todas as interfaces implementadas.
- uma classe abstrata não é obrigada a implementar todos os métodos definidos na interface. Porém, em uma classe concreta, é obrigatório.
- todos os atributos e métodos de uma interface são implicitamente públicos. Todo atributo em uma interface é implicitamente público, final e estático (Constante). Como esses qualificadores são fixos, não precisamos declará-los.

~~~java
public interface Autenticavel {
    String MSG_LOGOUT = "Saindo";

    boolean login(String usuario, String senha);

    void logout();
  }
~~~

~~~java
public class Usuario implements Autenticavel {
	
	@Override
	public boolean login(String usuario, String senha) {
		// TODO Auto-generated method stub
		return false;
	}
	
	@Override
	public void logout() {
		// TODO Auto-generated method stub
	}
}
~~~

- como a classe Usuario implementa a interface Autenticavel, ela deve implementar todos os métodos definidos pela interface, senão teremos um erro de compilação.
- `se uma classe implementar mais de uma interface, devemos separá-las por vírgula`.
- e se uma classe implementar uma ou mais interfaces e estender uma classe, primeiro precisamos definir a herança:

~~~java
public class Usuario extends Pessoa implements Autenticavel {
  // Código...
}
~~~

- ***sempre utilizar interfaces quando for preciso prover operações comuns a classes de hierarquia diferentes!!!***
- utilizar interfaces permite o uso do polimorfismo. Por exemplo, duas classes que implementam uma mesma interface podem ser atribuídas a uma variável do tipo da Interface. Porém, a execução dependerá do tipo do objeto que essa variável armazena.
- podemos ter métodos concretos em uma interface, utilizando o modificador default; esses métodos serão herdados por todas as classes que implementarem a interface, não sendo necessário implementá-la na classe (as classes que implementarem a interface já receberão o método, sem precisar implementá-lo).
- Static é outro método que possui implementação em uma interface. 
  - a diferença entre o método default e o método estático é que o estático pertence à interface e não pode ser sobrescrito (para executar o método estático, devemos referenciar a interface e não a classe ou oobjeto).
  - um default method pode ser sobrescrito em uma classe e precisa de uma de suas instâncias para ser executada.
- em uma interface, podemos definir todos os tipos de métodos em conjunto: abstratos (sem implementação, que deverá ser implementado na classe), métodos defaults e métodos estáticos.
- podemos utilizar o operador `instance of` para verificar se um objeto é do tipo de uma interface ou de uma classe (herança). Esse operador retorna true se o objeto à esquerda do operador é do tipo da classe ou interface especificada à direita do operador.

---

## FAST TEST

### 1. Sobre a exceção NullPointerException, selecione a alternativa correta que representa o cenário em que ela pode acontecer.
> Ocorre quando se tenta acessar, em tempo de execução, o conteúdo de uma variável ou a propriedade de objeto que ainda não tenha sido instanciado na memória.

### 2. Em Java, uma exceção pode ser classificada como:
> Checked, Unchecked e Error.

### 3. Respectivamente, qual é a função esperada de um Output stream e um Input stream:
> Realiza a gravação de um arquivo e realiza a leitura de um arquivo.

### 4. Uma exceção polimórfica do tipo Unchecked pode ser classificada como:
> Pode ser tratada pelo desenvolvedor ou relançada para o fluxo de execução.

### 5. Através do polimorfismo é possível estender classes e reaproveitar funcionalidades já implementadas. Dentro desse conceito, qual alternativa a seguir descreve a função de uma classe abstrata na linguagem Java.
> A classe abstrata não pode ser instanciada diretamente, ou seja, não pode ser utilizada para a criação de novos objetos na memória.

### 6. Em relação aos famosos blocos try-catch e try-catch-finally, no ambiente de desenvolvimento Java, podemos afirmar, verdadeiramente, que:
> São estruturas de captura e tratamento das exceções de tipo Checked e Unchecked.

### 7. A exceção IOException é lançada pela JVM em qual momento da execução do código-fonte?
> É uma exceção lançada, normalmente, quando se está lendo ou gravando dados em um arquivo.

### 8. Escolha a alternativa que representa a principal diferença entre uma classe e uma interface no ambiente Java.
> A interface é um contrato estabelecido com o objetivo de definir requisitos às classes que forem implementá-lo.

### 9. Selecione a alternativa que representa o fluxo convencional de captura de uma exceção no ambiente de desenvolvimento utilizando a linguagem Java.
> Exceção lançada, exceção capturada e tratamento realizado.

--- 

[Voltar ao início!](https://github.com/DigouO/Fintech_FIAP_2023)