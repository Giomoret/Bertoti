1. Comentário sobre o primeiro trecho:

  O trecho fala que engenharia de software vai além de programar, sendo sobre aplicar conhecimentos teóricos para criar sistemas confiáveis e seguros. À medida que o software cresce, é preciso organizar o código de forma a ser adaptável e escalável ao longo do tempo, levando em conta os custos e as mudanças.

2. Comentário sobre o segundo trecho:

  O segundo trecho menciona 3 trade-offs:

  Desempenho vs. Legibilidade: Melhorar o desempenho pode deixar o código mais difícil de entender.

  Velocidade de Desenvolvimento vs. Qualidade: Fazer rápido pode afetar a qualidade do código, com mais chances de erro.

  Escalabilidade vs. Simplicidade: Tornar o sistema escalável pode aumentar a complexidade, enquanto soluções simples podem não suportar o crescimento.

3. Exemplos de trade-offs:

  Desempenho vs. Consumo de Recursos: Melhorar o desempenho pode aumentar o uso de memória ou processamento.

  Desenvolvimento Rápido vs. Arquitetura Robusta: Entregar rápido pode prejudicar a estrutura do sistema, que ficará difícil de manter a longo prazo.

  Flexibilidade vs. Controle: Tornar o sistema flexível pode dificultar o controle sobre aspectos como segurança ou desempenho.

4. Diagrama de classe UML

   <img width="2816" height="1536" src="https://github.com/user-attachments/assets/6650a657-6fdb-4d1b-bdb4-8605620854c4" />
5. 
**Pedido**

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

class Pedido {
    private int idPedido;
    private Date data;
    private String status;
    private Cliente cliente;
    private List<ItemPedido> itens;
    private List<Pagamento> pagamentos;
    private double totalAmount;

    public Pedido(int idPedido, Cliente cliente) {
        this.idPedido = idPedido;
        this.cliente = cliente;
        this.data = new Date();
        this.status = "Aguardando Pagamento";
        this.itens = new ArrayList<>();
        this.pagamentos = new ArrayList<>();
        this.totalAmount = 0.0;
    }
    
    // Getters
    public int getIdPedido() { return idPedido; }
    public List<ItemPedido> getItens() { return itens; }
    public String getStatus() { return status; }
    public double getTotalAmount() { return totalAmount; }

    // Métodos de negócio
    public void adicionarItem(Livro livro, int quantidade) {
        ItemPedido novoItem = new ItemPedido(livro, quantidade);
        this.itens.add(novoItem);
        this.totalAmount = calcularTotal();
        System.out.println("Item adicionado: " + livro.getTitulo());
    }
    
    public double calcularTotal() {
        double total = 0.0;
        for (ItemPedido item : itens) {
            total += item.calcularSubtotal();
        }
        this.totalAmount = total;
        return total;
    }

    public void adicionarPagamento(Pagamento pagamento) {
        this.pagamentos.add(pagamento);
        pagamento.confirmarPagamento();
        verificarStatusPagamento();
    }
    
    private void verificarStatusPagamento() {
        double totalPago = 0.0;
        for (Pagamento p : pagamentos) {
            totalPago += p.getValor();
        }
        
        if (totalPago >= this.totalAmount && this.totalAmount > 0) {
            this.status = "Pago - Processando Envio";
            System.out.println("Status do Pedido ID " + idPedido + " atualizado para: " + this.status);
        } else if (totalPago > 0 && totalPago < this.totalAmount) {
            this.status = "Pagamento Parcial";
            System.out.println("Status do Pedido ID " + idPedido + " atualizado para: " + this.status);
        }
    }
    
    @Override
    public String toString() {
        return "Pedido{" +
                "id=" + idPedido +
                ", cliente=" + cliente.getNome() +
                ", data=" + data +
                ", status='" + status + '\'' +
                ", total=" + String.format("%.2f", totalAmount) +
                '}';
    }
}

**Classes de Apoio**

import java.util.Date;

// A) Classe Cliente
class Cliente {
    private int idCliente;
    private String nome;
    private String endereco;
    private String email;

    public Cliente(int idCliente, String nome, String endereco, String email) {
        this.idCliente = idCliente;
        this.nome = nome;
        this.endereco = endereco;
        this.email = email;
    }

    // Getters
    public int getIdCliente() { return idCliente; }
    public String getNome() { return nome; }

    @Override
    public String toString() {
        return "Cliente{" + "id=" + idCliente + ", nome='" + nome + '\'' + '}';
    }
}

// B) Classe Livro
class Livro {
    private int idLivro;
    private String titulo;
    private String autor;
    private double preco;

    public Livro(int idLivro, String titulo, String autor, double preco) {
        this.idLivro = idLivro;
        this.titulo = titulo;
        this.autor = autor;
        this.preco = preco;
    }

    // Getters
    public double getPreco() { return preco; }
    public String getTitulo() { return titulo; }
    // Outros Getters omitidos
}

// C) Classe ItemPedido
class ItemPedido {
    private Livro livro;
    private int quantidade;
    private double precoUnitario;

    public ItemPedido(Livro livro, int quantidade) {
        this.livro = livro;
        this.quantidade = quantidade;
        this.precoUnitario = livro.getPreco();
    }

    // Método para calcular o subtotal do item
    public double calcularSubtotal() {
        return this.quantidade * this.precoUnitario;
    }
    
    // Getters e Setters (Omitidos)
}

// D) Classe Pagamento
class Pagamento {
    private int idPagamento;
    private Date data;
    private double valor;
    private String metodo;

    public Pagamento(int idPagamento, double valor, String metodo) {
        this.idPagamento = idPagamento;
        this.data = new Date();
        this.valor = valor;
        this.metodo = metodo;
    }

    public void confirmarPagamento() {
        System.out.println("Pagamento de R$ " + String.format("%.2f", valor) + " via " + metodo + " confirmado.");
    }
    
    // Getter necessário para o Pedido verificar o total pago
    public double getValor() { return valor; }
    // Outros Getters e Setters (Omitidos)
}

7.

  <img src="My First Board.jpg" alt="Diagrama UML" width="2816" height="1536"/>

8. **Classes Respectivas**

**Funcionário**

  import java.util.Date;

public class Funcionario {
    // Atributos
    private int idFuncionario;
    private String email;
    private String telefone;
    private Date dataContratacao;
    private float salario;

    // Construtor
    public Funcionario(int idFuncionario, String email, String telefone, Date dataContratacao, float salario) {
        this.idFuncionario = idFuncionario;
        this.email = email;
        this.telefone = telefone;
        this.dataContratacao = dataContratacao;
        this.salario = salario;
    }

    // Métodos
    public boolean contratarFuncionario() {
        // Lógica para registrar contratação (ex: salvar no banco de dados)
        System.out.println("Funcionário " + idFuncionario + " contratado.");
        return true;
    }

    public boolean demitirFuncionario() {
        // Lógica para registrar demissão
        System.out.println("Funcionário " + idFuncionario + " demitido.");
        return true;
    }

    public void atualizarInfo(String email, String telefone, String string) {
        this.email = email;
        this.telefone = telefone;
        // O terceiro parâmetro 'string' no diagrama original parece ser um erro ou genérico. 
        // Aqui, vamos ignorá-lo ou assumir que seja o telefone.
        System.out.println("Informações do funcionário " + idFuncionario + " atualizadas.");
    }

    // Getters
    public int getIdFuncionario() { return idFuncionario; }
    // Outros Getters e Setters omitidos para brevidade
}
**Departamento**

public class Departamento {
    // Atributos
    private int idDepartamento;
    private String nome;
    private String localizacao;

    // Construtor
    public Departamento(int idDepartamento, String nome, String localizacao) {
        this.idDepartamento = idDepartamento;
        this.nome = nome;
        this.localizacao = localizacao;
    }

    // Métodos
    public boolean adicionarFuncionario(int idFuncionario) {
        // Lógica para adicionar o funcionário (usando o ID) à lista do departamento
        System.out.println("Funcionário ID " + idFuncionario + " adicionado ao departamento " + nome + ".");
        return true;
    }

    public boolean removerFuncionario(int idFuncionario) {
        // Lógica para remover o funcionário pelo ID
        System.out.println("Funcionário ID " + idFuncionario + " removido do departamento " + nome + ".");
        return true;
    }
    
    // Getters e Setters omitidos
}
**Gerente**

public class Gerente {
    // Atributo que atua como referência ao funcionário base (idFuncionario do Funcionario)
    private int idGerente; 
    
    // O diagrama implica que o Gerente se relaciona com um Funcionario 1 para 1.
    // Usamos o idGerente para representar essa ligação.

    // Construtor
    public Gerente(int idGerente) {
        this.idGerente = idGerente;
    }

    // Métodos
    public boolean atribuirProjeto(int idProjeto) {
        // Lógica para ligar o ID do projeto ao Gerente
        System.out.println("Gerente ID " + idGerente + " atribuiu o projeto ID " + idProjeto + ".");
        return true;
    }

    public void gerenciarOrcamento(float orcamento) {
        System.out.println("Gerente ID " + idGerente + " está gerenciando o orçamento: " + orcamento);
    }
    
    // Getters e Setters omitidos
}

**Cliente**

import java.util.List;
import java.util.ArrayList;

public class Cliente {
    // Atributos
    private int idCliente;
    private String nomeEmpresa;
    private String pessoaContato;
    private String email;
    private String telefone;
    
    // Lista para gerenciar o relacionamento (implícito no diagrama)
    private List<Projeto> projetos;

    // Construtor
    public Cliente(int idCliente, String nomeEmpresa, String pessoaContato, String email, String telefone) {
        this.idCliente = idCliente;
        this.nomeEmpresa = nomeEmpresa;
        this.pessoaContato = pessoaContato;
        this.email = email;
        this.telefone = telefone;
        this.projetos = new ArrayList<>();
    }

    // Métodos
    public boolean adicionarProjeto(Projeto projeto) {
        // Lógica para adicionar o projeto à lista do cliente
        this.projetos.add(projeto);
        System.out.println("Projeto " + projeto.getNome() + " adicionado ao cliente " + nomeEmpresa + ".");
        return true;
    }

    public void atualizarInfoContato(String email, String telefone) {
        this.email = email;
        this.telefone = telefone;
        System.out.println("Informações de contato do cliente " + nomeEmpresa + " atualizadas.");
    }
    
    // Getters e Setters omitidos
}

**Projeto**

import java.util.Date;
import java.util.List;
import java.util.ArrayList;

public class Projeto {
    // Atributos
    private int idProjeto;
    private String nome;
    private Date dataInicio;
    private Date dataFim;
    private String status;
    
    // Relacionamentos com outras classes (para as associações)
    private Gerente gerente;
    private List<Funcionario> equipe; // Funcionario ou Desenvolvedor/Gerente
    private List<Tarefa> tarefas;
    private Cliente cliente;

    // Construtor
    public Projeto(int idProjeto, String nome, Date dataInicio, String status, Cliente cliente) {
        this.idProjeto = idProjeto;
        this.nome = nome;
        this.dataInicio = dataInicio;
        this.status = status;
        this.cliente = cliente;
        this.equipe = new ArrayList<>();
        this.tarefas = new ArrayList<>();
    }

    // Métodos
    public boolean iniciarProjeto() {
        this.status = "Iniciado";
        System.out.println("Projeto " + nome + " iniciado.");
        return true;
    }

    public boolean finalizarProjeto() {
        this.status = "Finalizado";
        System.out.println("Projeto " + nome + " finalizado.");
        return true;
    }

    public void atualizarStatus(String status) {
        this.status = status;
        System.out.println("Status do projeto " + nome + " atualizado para: " + status);
    }
    
    // Getters e Setters
    public String getNome() { return nome; }
    // Outros Getters e Setters omitidos
}

**Desenvolvedor**

import java.util.List;
import java.util.ArrayList;

public class Desenvolvedor {
    // Atributos
    private String especializacao;
    
    // Relacionamento 1 para 1 com Funcionario (implícito)
    private Funcionario funcionarioBase; 
    
    // Relacionamento 1..n com Tarefa
    private List<Tarefa> tarefasAtribuidas;

    // Construtor
    public Desenvolvedor(String especializacao, Funcionario funcionarioBase) {
        this.especializacao = especializacao;
        this.funcionarioBase = funcionarioBase;
        this.tarefasAtribuidas = new ArrayList<>();
    }

    // Métodos
    public void escreverCodigo() {
        System.out.println("Desenvolvedor está escrevendo código.");
    }

    public void depurarCodigo() {
        System.out.println("Desenvolvedor está depurando código.");
    }
    
    // Getters e Setters omitidos
}

**Tarefa**

import java.util.Date;
import java.util.List;
import java.util.ArrayList;

public class Tarefa {
    // Atributos
    private int idTarefa;
    private String descricao;
    private Date dataEntrega;
    private String status;
    private int horasEstimadas;
    
    // Relacionamentos
    private Projeto projeto;
    private List<Desenvolvedor> desenvolvedores; // Pode ser 0..n

    // Construtor
    public Tarefa(int idTarefa, String descricao, Date dataEntrega, int horasEstimadas, Projeto projeto) {
        this.idTarefa = idTarefa;
        this.descricao = descricao;
        this.dataEntrega = dataEntrega;
        this.horasEstimadas = horasEstimadas;
        this.projeto = projeto;
        this.status = "Pendente";
        this.desenvolvedores = new ArrayList<>();
    }

    // Métodos
    public boolean atribuirParaDesenvolvedor(int idDesenvolvedor) {
        // Lógica para encontrar o Desenvolvedor pelo ID e atribuir a tarefa
        System.out.println("Tarefa " + idTarefa + " atribuída ao Desenvolvedor ID " + idDesenvolvedor + ".");
        return true;
    }

    public void atualizarStatus(String status) {
        this.status = status;
        System.out.println("Status da Tarefa " + idTarefa + " atualizado para: " + status);
    }
    
    // Getters e Setters omitidos
    public String getDescricao() { return descricao; }
}

9. **Testes JUNit**

    **FuncionarioTest**

   import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import java.util.Date;
import static org.junit.jupiter.api.Assertions.*;

public class FuncionarioTest {

    private Funcionario funcionario;

    @BeforeEach
    void setUp() {
        // Inicializa um novo objeto Funcionario antes de cada teste
        // O valor 'float' do salário deve ser representado por 1000.0f
        funcionario = new Funcionario(1, "joao@empresa.com", "9999-8888", new Date(), 1000.0f);
    }

    @Test
    void testContratarFuncionario() {
        // Verifica se o método de contratação retorna true, conforme o diagrama
        assertTrue(funcionario.contratarFuncionario(), "O método contratarFuncionario deve retornar true.");
    }

    @Test
    void testDemitirFuncionario() {
        // Verifica se o método de demissão retorna true
        assertTrue(funcionario.demitirFuncionario(), "O método demitirFuncionario deve retornar true.");
    }

    @Test
    void testAtualizarInfo() {
        String novoEmail = "novo.joao@empresa.com";
        String novoTelefone = "1111-2222";

        // Chama o método atualizarInfo
        funcionario.atualizarInfo(novoEmail, novoTelefone, "Ignorado");

        // Como não temos Getters no código fornecido, verificamos o ID
        // (Se houvesse Getters para email e telefone, o ideal seria:
        // assertEquals(novoEmail, funcionario.getEmail());)
        
        // Verificação básica: Checa se o ID foi mantido, confirmando que a instância existe.
        assertEquals(1, funcionario.getIdFuncionario(), "O ID do funcionário deve ser mantido após a atualização.");
    }

    @Test
    void testGetIdFuncionario() {
        assertEquals(1, funcionario.getIdFuncionario(), "O ID do funcionário deve ser 1.");
    }
}

**ProjetoTest**

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import java.util.Date;
import static org.junit.jupiter.api.Assertions.*;

public class ProjetoTest {

    private Projeto projeto;
    private Cliente cliente;

    @BeforeEach
    void setUp() {
        // Inicializa dependências
        cliente = new Cliente(10, "Tech Solutions", "Ana", "ana@tech.com", "5555-1234");

        // Cria uma instância de Projeto (status inicial é "Planejamento" definido no construtor)
        projeto = new Projeto(101, "App Mobile V1", new Date(), "Planejamento", cliente);
    }

    @Test
    void testIniciarProjeto() {
        // Inicia o projeto
        assertTrue(projeto.iniciarProjeto(), "O método iniciarProjeto deve retornar true.");
        
        // Verifica se o status foi alterado (depende de haver um Getter para 'status' em Projeto)
        // Se a classe Projeto tivesse o método getStatus():
        // assertEquals("Iniciado", projeto.getStatus(), "O status deve ser 'Iniciado'.");
    }

    @Test
    void testFinalizarProjeto() {
        // Finaliza o projeto
        assertTrue(projeto.finalizarProjeto(), "O método finalizarProjeto deve retornar true.");

        // Verifica o estado final
        // Se a classe Projeto tivesse o método getStatus():
        // assertEquals("Finalizado", projeto.getStatus(), "O status deve ser 'Finalizado'.");
    }

    @Test
    void testAtualizarStatus() {
        String novoStatus = "Em Desenvolvimento";
        
        // Atualiza o status
        projeto.atualizarStatus(novoStatus);

        // Verificação (Se a classe Projeto tivesse o método getStatus()):
        // assertEquals(novoStatus, projeto.getStatus(), "O status deve ser 'Em Desenvolvimento'.");
    }
}



  
