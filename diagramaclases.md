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
stateDiagram-v2
    [*] --> Inicializando
    
    Inicializando --> EsperandoEntrada : página cargada<br/>listeners configurados
    
    EsperandoEntrada --> CapturandoFormula : usuario escribe<br/>en input
    EsperandoEntrada --> SeleccionBotonRapido : click en botón<br/>rápido (1d6, 1d20...)
    EsperandoEntrada --> LanzandoMoneda : click en botón<br/>MONEDA
    
    CapturandoFormula --> ValidandoEntrada : presiona LANZAR<br/>o tecla Enter
    SeleccionBotonRapido --> ValidandoEntrada : fórmula<br/>auto-establecida
    
    ValidandoEntrada --> ErrorEntradaVacia : input vacío
    ValidandoEntrada --> ParseandoFormula : input no vacío
    
    ParseandoFormula --> ErrorFormatoInvalido : formato incorrecto<br/>(regex no coincide)
    ParseandoFormula --> ExtrayendoComponentes : formato válido<br/>(XdY+Z)
    
    ExtrayendoComponentes --> ValidandoNumDados : componentes<br/>extraídos
    
    ValidandoNumDados --> ErrorRangoDados : numDice < 1<br/>o > 100
    ValidandoNumDados --> ValidandoCarasDado : numDice OK<br/>(1-100)
    
    ValidandoCarasDado --> ErrorRangoCaras : diceSides < 2<br/>o > 1000
    ValidandoCarasDado --> GenerandoNumeros : diceSides OK<br/>(2-1000)
    
    GenerandoNumeros --> CalculandoSuma : todos los dados<br/>lanzados
    
    CalculandoSuma --> AplicandoModificador : suma calculada
    
    AplicandoModificador --> CreandoResultado : total calculado
    
    CreandoResultado --> MostrandoResultado : objeto DiceResult<br/>creado
    
    LanzandoMoneda --> GenerandoAleatorioMoneda : ejecutando<br/>flipCoin()
    
    GenerandoAleatorioMoneda --> DeterminandoCara : random < 0.5
    GenerandoAleatorioMoneda --> DeterminandoCruz : random >= 0.5
    
    DeterminandoCara --> MostrandoResultadoMoneda : CARA 🪙
    DeterminandoCruz --> MostrandoResultadoMoneda : CRUZ ⚫
    
    ErrorEntradaVacia --> MostrandoError : mensaje:<br/>"Introduce una fórmula"
    ErrorFormatoInvalido --> MostrandoError : mensaje:<br/>"Formato inválido"
    ErrorRangoDados --> MostrandoError : mensaje:<br/>"1-100 dados"
    ErrorRangoCaras --> MostrandoError : mensaje:<br/>"2-1000 caras"
    
    MostrandoError --> EsperandoEntrada : error mostrado<br/>sistema listo
    MostrandoResultado --> EsperandoEntrada : resultado mostrado<br/>historial actualizado
    MostrandoResultadoMoneda --> EsperandoEntrada : resultado mostrado<br/>historial actualizado
    
    EsperandoEntrada --> [*] : usuario cierra<br/>página
    
    note right of Inicializando
        - Cargar DOM
        - Crear referencias
        - Configurar eventos
    end note
    
    note right of ValidandoEntrada
        Verifica que el input
        no esté vacío antes
        de procesar
    end note
    
    note right of ParseandoFormula
        Regex: /^(\d+)d(\d+)([\+\-]\d+)?$/
        Ejemplo: 2d6+3
    end note
    
    note right of GenerandoNumeros
        Loop: para cada dado
        Math.floor(Math.random() * sides) + 1
    end note
    
    note right of MostrandoResultado
        HTML generado:
        - Fórmula
        - Dados individuales
        - Modificador (si existe)
        - Total final
    end note
```
