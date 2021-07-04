/*
SPDX-License-Identifier: CC-BY-4.0
SmartContract para atribuição de nota - Feito por Elayne Nascimento 
*/ 
pragma solidity 0.8.4;

contract PrestacaoDeServicosDeTelefonia {
    
    struct ServicoContratado { //Estrutura com os dados personalizados necessários para realização do contrato
        string NomeDaContratante; //Nome da contratante
        uint IdadeDaContratante; //Idade da contratante
        uint CPFdaContratante; //CPF da contratante
        bool ClienteAntigo; // Cliente possui outros produtos da companhia? True=Sim, cliente antigo / False=Não cliente novo
        }
        
    uint constant valormensaldocontrato = 250; //Constante com o valor inicial do contratos
    uint constant mesesdefidelidade = 12; //constante com os 12 meses de mesesdefidelidade
    uint constant descontoClienteAntigo = 5; // constante com 5% de desconto para clientes que já possuem outros produtos da companhia
        
        address public owner;
        
        ServicoContratado[] public Servicos; 
        //Array - Criação de uma pasta com os dados da estrutura do Serviço Contratado, declarado acima em "Struct"
        
    struct Contratada { //Estrutura com os dados cadastrais da empresa contratada
        string NomeDaEmpresa; 
        string Endereco;
        uint CNPJ;
        }
    
    constructor() {
        owner = msg.sender; //Atribuição da publicação do contrato ao proprietário do contrato, ninguém mais pode publicar um contrato.
        }
    
    function RegistroServicoContratado( //Função para criação de variáveis externas para registro do contrato
        string memory CampoNomeContratante
        ,uint CampoIdadeContratante
        ,uint CampoCPFContratante
        ,bool CampoClienteAntigo
    ) 
    
    external returns (bool) { 
        //Função pública destinada aos usuários do sistema para preenchimento dos dados pessoais para o contrato
        //Retorno booleano para confirmação do envio dos dados (true)
        require(msg.sender == owner, "Somente o proprietario do contrato pode registrar novos contratos");
        //Requerimento que permite apenas o registro de um novo contrato pelo proprietário  
        require(CampoIdadeContratante >= 18, "A contratante deve possuir mais de 18 anos");
        //Requerimento que permite apenas a publicação de um novo contrato para clientes com idade igual ou superior à 18 anos
        ServicoContratado memory NovoContrato = ServicoContratado(CampoNomeContratante, CampoIdadeContratante, CampoCPFContratante, CampoClienteAntigo);
        //Criação das variáveis na estrutura do Serviço Contratado
     Servicos.push(NovoContrato);
     //Registro das variáveis na biblioteca "Array"
     return true;
     //Confirmação da operação realizada com sucesso.
    }
    
    }    
