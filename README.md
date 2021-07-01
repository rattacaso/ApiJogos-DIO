# ApiJogos-DIO - Digital Innovation One
https://digitalinnovation.one/
Atividade prática para criação de API. ASP.NET Core Web Application[Web API]
# ApiCatalogoJogos

Replicação do Projeto da aula API Rest da DIGITAL INOVATION ONE.

Adicional: Configurando registro de logs utilizando o Serilog. Pacote instalado utilizando o gerenciador NuGet.

Serilog.Asp.NetCore-4,1,1-dev-00229

Exemplo de utilização no arquivo: Program.cs


using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Serilog;
using Serilog.Events;

namespace ExemploApiCatalogoJogos
{
    public class Program
    {
        public static void Main(string[] args)
        { 
            Log.Logger = new LoggerConfiguration()
                .WriteTo.File(
                    //No linux, o path da pasta onde está armazenando os logs:
                    path: "/home/Rafael/apiJogos/logs/log-.txt", 
                    // No Windows: Exemplo do path: C:\\MeusLogs\\ApiJogos\\log-.txt
                    // na pasta, será armazenado com a data após o -. EXEMPLO: log-20210630.txt
                    // RESUMINDO: SERÁ CRIADO UM DIRETÓRIO PARA ARMAZENAR OS LOGS DA API ATRAVÉS DO
                    // PACOTE: Serilog.Asp.NetCore-4,1,1-dev-00229
                    outputTemplate:
                    $"{{Timestamp:yyyy-MM-dd HH:mm:ss.fff zzz}} [{{Level:u3}}] {{Message:1j}}{{NewLine}}{{Exception}}",
                    rollingInterval: RollingInterval.Day,
                    restrictedToMinimumLevel: LogEventLevel.Information
                ).CreateLogger();
            try
            {
                Log.Information("Application Is Starting");
                CreateHostBuilder(args).Build().Run();
            }
            catch (Exception e)
            {
                Log.Information("Application Failed to start");
            }
            finally
            {
                Log.CloseAndFlush();
            }
        }

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .UseSerilog()
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseStartup<Startup>();
                });
    }
}



# CriacaodeApiDotNet


