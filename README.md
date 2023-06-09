# AcademiaProjectoWebApiNetCore6

- Web API ASPNET Core 6.0
- EF Core

## Requisitos
- Instalar SQL Server Express local ou em uma imagem docker
  - link https://go.microsoft.com/fwlink/p/?linkid=2216019&clcid=0x416&culture=pt-br&country=br
- Ativar usuario do banco de dados (ativei o usuario sa
  - link https://www.secullum.com.br/pt/canal-cliente/perguntas/766#:~:text=Para%20habilitarmos%20esse%20usu%C3%A1rio%2C%20siga%20os%20procedimentos%20abaixo%3A,sobre%20a%20conex%C3%A3o%20e%20localize%20o%20item%20Propriedades%3A
  
- Instalação de Pacotes NUGET
  - EntityFrameworkeCore
  - EntityFrameworkeCore.design
  - EntityFrameworkeCore.SqlServer
  - EntityFrameworkeCore.Tools

## Pastas do projeto
- 1.UI
  - Aqui será construído o projeto front-end 
- 2.WebApi
  - AcademiaProjeto.WebApi
- 3.Domain
  - Aqui ficam as entidades de dominio
  - AcademiaProjeto.Domain
- 4.Repository
  - AcademiaProjeto.Repositories
- 5.Data
  - AcademiaProjeto.Data

## Conexão da base dados

## Passo a passo
- Criação do projeto web api ASPNET Core .Net6
- Criação da biblioteca de classe AcademiaProjeto.Data
  - Instalação dos pacotes do entity framework core
  - Criação da pasta Context
  - Criação da classe DataContext
  - override do método OnModelCreating na classe DataContext
    - setando as entidades que fazem parte modelBuilder.Entity<Curso>(new CursoConfiguration().Configure);
  - Criação da classe CursoConfiguration
    - Implementando interface IEntityTypeConfiguration<Curso>
	- override do método Configure que detalha as colunas da tabela curso
- Criação da biblioteca de classe AcademiaProjeto.Domain  
  - Criação da pasta Entities
  - Criação da classe Curso
- Criação do biblioteca de classe AcademiaProjeto.Repository
  - Criação da pasta Base
	- Criação da interface IBaseRepository<T> where T : class com as assinaturas do metodos
    - Criação da classe BaseRepository<T> : IBaseRepository<T> where T : class
	- Implentação dos métodos genéricos na classe
  - Criação da pasta Interface
    - Criação da interface  ICursoRepository : IBaseRepository<Curso>
  - Criação da Pasta Repository  
    - Criação da classe CursoRepository : BaseRepository<Curso>, ICursoRepository e seu construtor recebendo DataContext
- Edição do appSettings.json
  - Adicionada "ConnectionStrings" : { "DefaultConnection" : "Data Source=localhost
- Edição Program.cs. Adicionado carregamento da string de conexão string strConnection = builder.Configuration.GetConnectionString("DefaultConnection");
  - Adicionada Injeção builder.Services.AddDbContext<DataContext>(option => 
{
    option.UseSqlServer(strConnection);
});
  - builder.Services.AddScoped<ICursoRepository, CursoRepository>();
- Console Gerenciador de Pacotes: add-migration CreateTableCursos
- Console Gerenciador de Pacotes: update-database
- Execução da API

## Imagens do projeto

![conectar no banco](https://github.com/suarezrafael/AcademiaProjectoWebApiNetCore6/blob/main/docs/1.JPG)
![conectar no banco 2](https://github.com/suarezrafael/AcademiaProjectoWebApiNetCore6/blob/main/docs/2.JPG)
![solution vision](https://github.com/suarezrafael/AcademiaProjectoWebApiNetCore6/blob/main/docs/3.JPG)

asd