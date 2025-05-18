# Sistema-estacionamento
using System;
using System.Collections.Generic;

namespace Estacionamento
{
    public class Veiculo
    {
        public string Placa { get; set; }
        public DateTime HoraEntrada { get; set; }
    }

    public class Estacionamento
    {
        private List<Veiculo> veiculos = new List<Veiculo>();
        private decimal precoInicial = 0;
        private decimal precoPorHora = 0;

        public Estacionamento(decimal precoInicial, decimal precoPorHora)
        {
            this.precoInicial = precoInicial;
            this.precoPorHora = precoPorHora;
        }

        public void AdicionarVeiculo()
        {
            Console.WriteLine("Digite a placa do veículo para estacionar:");
            string placa = Console.ReadLine();
            
            veiculos.Add(new Veiculo {
                Placa = placa,
                HoraEntrada = DateTime.Now
            });
            
            Console.WriteLine($"Veículo {placa} adicionado com sucesso!");
        }

        public void RemoverVeiculo()
        {
            Console.WriteLine("Digite a placa do veículo para remover:");
            string placa = Console.ReadLine();

            Veiculo veiculo = veiculos.Find(v => v.Placa.Equals(placa));
            
            if (veiculo != null)
            {
                Console.WriteLine("Digite a quantidade de horas que o veículo permaneceu estacionado:");
                int horas = int.Parse(Console.ReadLine());
                
                decimal valorTotal = precoInicial + (precoPorHora * horas);
                
                veiculos.Remove(veiculo);
                
                Console.WriteLine($"O veículo {placa} foi removido e o preço total foi de: R$ {valorTotal}");
            }
            else
            {
                Console.WriteLine("Desculpe, esse veículo não está estacionado aqui. Confira se digitou a placa corretamente");
            }
        }

        public void ListarVeiculos()
        {
            if (veiculos.Count > 0)
            {
                Console.WriteLine("Os veículos estacionados são:");
                
                foreach (var veiculo in veiculos)
                {
                    Console.WriteLine($"Placa: {veiculo.Placa} - Entrada: {veiculo.HoraEntrada}");
                }
            }
            else
            {
                Console.WriteLine("Não há veículos estacionados.");
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Seja bem vindo ao sistema de estacionamento!\n" +
                            "Digite o preço inicial:");
            decimal precoInicial = decimal.Parse(Console.ReadLine());

            Console.WriteLine("Agora digite o preço por hora:");
            decimal precoPorHora = decimal.Parse(Console.ReadLine());

            Estacionamento estacionamento = new Estacionamento(precoInicial, precoPorHora);

            bool exibirMenu = true;

            while (exibirMenu)
            {
                Console.WriteLine("\nDigite a sua opção:");
                Console.WriteLine("1 - Cadastrar veículo");
                Console.WriteLine("2 - Remover veículo");
                Console.WriteLine("3 - Listar veículos");
                Console.WriteLine("4 - Encerrar");

                switch (Console.ReadLine())
                {
                    case "1":
                        estacionamento.AdicionarVeiculo();
                        break;
                    case "2":
                        estacionamento.RemoverVeiculo();
                        break;
                    case "3":
                        estacionamento.ListarVeiculos();
                        break;
                    case "4":
                        exibirMenu = false;
                        break;
                    default:
                        Console.WriteLine("Opção inválida");
                        break;
                }
            }

            Console.WriteLine("O programa se encerrou");
        }
    }
}
