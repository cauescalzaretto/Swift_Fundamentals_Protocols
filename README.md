# Swift Fundamentals Protocols

    //: Playground - noun: a place where people can play
    
    import UIKit
    
    //---------------------------------------------------------------
    //: Author - Cauê Scalzaretto
    //: Site - http://www.cauescalzaretto.com
    //: GitHub - https://github.com/cauescalzaretto
    //---------------------------------------------------------------
    
    //=================================================================================================
    // Protocolos são os requerimentos necessários para uma classe, estrutura ou enumeração
    // determinando os objetos, métodos e propriedades que serão necessários para a sua criação.
    // Sempre a classe, estrutura ou enumeração deve estar em conformidade com o protocolo seguido,
    // ou seja, o protocolo realmente determinará quais tarefas deverão ser completadas dentro desse(s) padrão(s)
    //=================================================================================================
    
    
    //--------------------------------
    //EXEMPLO 1
    //--------------------------------
    // O protocolo Pao irá definir e exigir todas as variavel criadas
    protocol Pao
    {
        var nome : String {get set}
        var farinha : Int {get set}
        var fermento : Int {get set}
        var leite : Int {get set}
    }
    
    class paoFrances: Pao
    {
        // Devemos especificar todos os itens pertencentes ao Protocolo Pao
        var nome: String
        var farinha: Int
        var fermento: Int
        var leite: Int
        
        // Metodo de inicializacao das propriedades desta classe
        init(sNome: String, iFarinha: Int, iFermento: Int, iLeite: Int)
        {
            nome = sNome
            farinha = iFarinha
            fermento = iFermento
            leite = iLeite
        }
    }
    
    //--------------------------------
    // EXEMPLO 2
    //--------------------------------
    // O protocolo RandomNumberGenerator solicita que se tenha um método que retorne uma numerção do tipo Double
    protocol RandomNumberGenerator
    {
        func random() -> Double
    }
    
    // A classe abaixo implementa o protocolo RandomNumberGenerator
    class LinearCongruentialGenerator: RandomNumberGenerator
    {
        // Propriedades da classe
        var lastRandom = 42.0
        let m = 139968.0
        let a = 3877.0
        let c = 29573.0
        
        // Este é o método exigido pelo protocolo, que retorna um número aleatório
        func random() -> Double
        {
            lastRandom = ((lastRandom * a + c).truncatingRemainder(dividingBy:m))
            
            return lastRandom / m
        }
    }
    
    // Criando um instância da classe
    let generator = LinearCongruentialGenerator()
    
    print("Um número qualquer: \(generator.random())")
    
    print("outro número qualquer: \(generator.random())")
    
    //--------------------------------
    // EXEMPLO 3
    //--------------------------------
    
    // A classe Dice permite que se role um dado e se tenha uma numeração conforme os parametros
    class Dice
    {
        // lados do dado
        let sides: Int
        
        // Utilizando o procotolo RandomNumberGenerator em um variável
        let generator: RandomNumberGenerator
        
        // Inicializando a classe tendo como parametro o protocolo RandomNumberGenerator
        init(sides: Int, generator: RandomNumberGenerator)
        {
            self.sides = sides
            self.generator = generator
        }
        
        // Este método retorna uma numeração entre 1 e o quantidade de lados do dado
        func roll() -> Int
        {
            // a propriedade generator que tem como tipagem o protocolo RandomNumberGenerator,
            // irá receber um número qualquer, onde multiplicando pelos lados do dado e somando
            // 1, temos uma numerção de 1 à quantidade de lados do dado
            return Int(generator.random() * Double(sides)) + 1
        }
        
    }
    
    // Criando uma variável que receberá um valor do tipo Int.
    // Criamos assim um dado de 6 lados, vejam que utilizamos a claaase LinearCongruentialGenerator
    // do exemplo anterior que adota o protocolo RandomNumberGenerator
    var d6 = Dice(sides: 6, generator: LinearCongruentialGenerator())
    
    for _ in 1...5 {
        print("Rolando o dado : \(d6.roll())")
    }

