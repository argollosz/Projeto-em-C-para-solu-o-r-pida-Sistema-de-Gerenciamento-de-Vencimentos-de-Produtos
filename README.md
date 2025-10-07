# Projeto-em-C-para-solu-o-r-pida-Sistema-de-Gerenciamento-de-Vencimentos-de-Produtos
Este código, embora simples, demonstra de forma eficaz a habilidade de estruturar um problema real em um situação onde separa objetos, responsabilidades, protegendo dados e implementando lógicas de negócio e de permissão de forma clara e organizada.



    public class Produto
    {
        public int Id { get; private set; }
        public string Nome { get; private set; }
        public DateTime DataVencimento { get; private set; }

        public Produto(int id, string nome, DateTime dataVencimento)
        {
            Id = id;
            Nome = nome;
            DataVencimento = dataVencimento;
        }

        public bool EstaVencido(DateTime dataAtual)
        {
            return DataVencimento < dataAtual;
        }
    }

    public class Funcionario
    {
        public int Id { get; private set; }
        public string Nome { get; private set; }
        public int Tipo { get; private set; }

        public Funcionario(int id, string nome, int tipo)
        {
            Id = id;
            Nome = nome;
            Tipo = tipo;
        }

        public void VerificarProdutosVencidos(List<Produto> produtos, DateTime dataAtual)
        {
            if (Tipo == 0)
            {
                Console.WriteLine($"Gerente {Nome} verificando produtos vencidos:");
                foreach (var produto in produtos)
                {
                    if (produto.EstaVencido(dataAtual))
                    {
                        Console.WriteLine($"Produto: {produto.Nome} (ID: {produto.Id}) está vencido. Data de Vencimento: {produto.DataVencimento.ToShortDateString()}");
                    }
                }
            }
            else
            {
                Console.WriteLine($"Funcionário {Nome} (Tipo: {Tipo}) não tem permissão para verificar produtos vencidos.");
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            List<Produto> produtos = new List<Produto>
        {
            new Produto(1, "Leite", new DateTime(2025, 9, 20)),
            new Produto(2, "Iogurte", new DateTime(2025, 9, 22)),
            new Produto(3, "Queijo", new DateTime(2025,9, 16))
        };

            Funcionario gerente = new Funcionario(1, "Ana", 0);
            Funcionario supervisor = new Funcionario(2, "Carlos", 1);
            Funcionario operador = new Funcionario(3, "Mariana", 2);

            DateTime dataAtual = DateTime.Now;

            gerente.VerificarProdutosVencidos(produtos, dataAtual);
            supervisor.VerificarProdutosVencidos(produtos, dataAtual);
            operador.VerificarProdutosVencidos(produtos, dataAtual);
        }
    }
}
