# Diagrama de clases
```mermaid
classDiagram
direction TB

class DiceRollerApp {
    -resultsDiv: HTMLElement
    -diceInput: HTMLInputElement
    +initialize() void
    +setupEventListeners() void
}

class UIController {
    -resultsDiv: HTMLElement
    -diceInput: HTMLInputElement
    +quickRoll(formula: String) void
    +rollDice() void
    +flipCoin() void
    +displayResult(result: DiceResult) void
    +showError(message: String) void
}

class DiceParser {
    +parseDiceFormula(formula: String) DiceResult
    -validateInput(formula: String) boolean
    -extractComponents(formula: String) FormulaComponents
}

class DiceRoller {
    +roll(numDice: int, diceSides: int) int[]
    -generateRandomNumber(min: int, max: int) int
    +calculateTotal(rolls: int[], modifier: int) int
}

class DiceResult {
    +formula: String
    +rolls: int[]
    +modifier: int
    +sum: int
    +total: int
    +diceSides: int
}

class FormulaComponents {
    +numDice: int
    +diceSides: int
    +modifier: int
}

class CoinFlipper {
    +flip() String
    -getRandomBoolean() boolean
}

class Validator {
    +validateDiceCount(numDice: int) void
    +validateDiceSides(diceSides: int) void
    +validateFormula(formula: String) void
}

class DiceRollerException {
    <<exception>>
    +message: String
}

%% Relaciones
DiceRollerApp --> UIController : controla
UIController --> DiceParser : usa
UIController --> CoinFlipper : usa
UIController --> DiceResult : muestra
DiceParser --> Validator : valida con
DiceParser --> DiceRoller : lanza con
DiceParser --> FormulaComponents : crea
DiceParser --> DiceResult : retorna
DiceRoller --> DiceResult : genera
Validator ..> DiceRollerException : lanza
DiceParser ..> DiceRollerException : propaga

%% Notas
note for DiceRollerApp "Punto de entrada de la aplicación\nInicializa componentes y eventos"
note for DiceParser "Analiza fórmulas tipo: XdY+Z\nEjemplo: 2d6+3"
note for Validator "Límites: 1-100 dados\n2-1000 caras por dado"
```

# Diagrama de secuencia
```mermaid
stateDiagram-v2
    [*] --> Inicial
    
    Inicial --> EsperandoEntrada : página cargada
    EsperandoEntrada --> ValidandoFormula : usuario ingresa fórmula
    EsperandoEntrada --> LanzandoMoneda : click en MONEDA
    
    ValidandoFormula --> ErrorFormato : formato inválido
    ValidandoFormula --> ValidandoRestricciones : formato válido
    
    ValidandoRestricciones --> ErrorRango : fuera de límites
    ValidandoRestricciones --> GenerandoDados : restricciones OK
    
    GenerandoDados --> CalculandoResultado : dados lanzados
    CalculandoResultado --> MostrandoResultado : cálculo completado
    
    LanzandoMoneda --> MostrandoResultado : cara o cruz
    
    ErrorFormato --> EsperandoEntrada : error mostrado
    ErrorRango --> EsperandoEntrada : error mostrado
    MostrandoResultado --> EsperandoEntrada : resultado mostrado
    
    EsperandoEntrada --> [*] : usuario cierra página
```
# Diagrama de Estados
```mermaid
sequenceDiagram
    autonumber
    
    actor Usuario
    participant Main as Main
    participant UI as UIController
    participant Input as DiceInput
    participant Parser as DiceParser
    participant Valid as Validator
    participant Roller as DiceRoller
    participant Result as DiceResult
    participant Display as ResultDisplay
    
    Usuario->>Main: Cargar página
    Main->>UI: initialize()
    UI->>UI: setupEventListeners()
    
    Usuario->>Input: Escribir fórmula
    Input-->>Usuario: fórmula capturada
    
    Usuario->>UI: Click LANZAR
    UI->>Input: obtenerValor()
    Input-->>UI: formula
    
    alt formula vacía
        UI->>Display: mostrarError("Por favor, introduce una fórmula de dados")
    else formula no vacía
        UI->>Parser: parseDiceFormula(formula)
        Parser->>Parser: limpiarFormula()
        Parser->>Parser: aplicarRegex()
        
        alt formato inválido
            Parser--xUI: Error("Formato inválido. Usa el formato: XdY+Z")
            UI->>Display: mostrarError("Formato inválido. Usa el formato: XdY+Z")
        else formato válido
            Parser->>Parser: extraerComponentes(numDice, diceSides, modifier)
            
            Parser->>Valid: validateDiceCount(numDice)
            alt numDice < 1 o numDice > 100
                Valid--xParser: Error("El número de dados debe estar entre 1 y 100")
                Parser--xUI: propagar error
                UI->>Display: mostrarError("El número de dados debe estar entre 1 y 100")
            else numDice válido
                Valid-->>Parser: OK
                
                Parser->>Valid: validateDiceSides(diceSides)
                alt diceSides < 2 o diceSides > 1000
                    Valid--xParser: Error("Los dados deben tener entre 2 y 1000 caras")
                    Parser--xUI: propagar error
                    UI->>Display: mostrarError("Los dados deben tener entre 2 y 1000 caras")
                else diceSides válido
                    Valid-->>Parser: OK
                    
                    Parser->>Roller: roll(numDice, diceSides)
                    Roller->>Roller: generarNumerosAleatorios()
                    Roller-->>Parser: rolls[]
                    
                    Parser->>Parser: calcularSuma(rolls)
                    Parser->>Parser: aplicarModificador(suma, modifier)
                    
                    Parser->>Result: new DiceResult(formula, rolls, modifier, suma, total)
                    Result-->>Parser: instancia creada
                    
                    Parser-->>UI: resultado
                    
                    opt resultado calculado correctamente
                        UI->>Display: displayResult(resultado)
                        Display->>Usuario: Mostrar resultado
                    end
                end
            end
        end
    end
```
