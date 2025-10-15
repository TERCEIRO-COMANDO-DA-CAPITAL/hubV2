# Documentação da redzlib v1.1.0

A **redzlib** é uma biblioteca Lua para criar interfaces gráficas (GUIs) em Roblox, com suporte a temas modernos como Amoled glassmorphism, botões personalizáveis, seletores de cores e dropdowns atualizáveis. Esta documentação cobre como usar, criar e atualizar elementos da interface, incluindo exemplos comentados e métodos disponíveis.

---

## Índice
1. [Visão Geral](#visão-geral)
2. [Instalação](#instalação)
3. [Criação de uma Janela](#criação-de-uma-janela)
4. [Métodos Disponíveis](#métodos-disponíveis)
   - [Janela (Window)](#janela-window)
   - [Aba (Tab)](#aba-tab)
   - [Seção (Section)](#seção-section)
   - [Parágrafo (Paragraph)](#parágrafo-paragraph)
   - [Botão (Button)](#botão-button)
   - [Toggle](#toggle)
   - [Dropdown](#dropdown)
   - [Slider](#slider)
   - [Caixa de Texto (TextBox)](#caixa-de-texto-textbox)
   - [Convite do Discord](#convite-do-discord)
   - [Seletor de Cores (ColorPicker)](#seletor-de-cores-colorpicker)
5. [Atualização de Elementos](#atualização-de-elementos)
   - [Atualizar Dropdowns](#atualizar-dropdowns)
6. [Exemplo Completo](#exemplo-completo)
7. [Notas Finais](#notas-finais)

---

## Visão Geral
A redzlib permite criar interfaces com temas visuais (Darker, Dark, Purple, Amoled) e elementos interativos como botões, toggles, dropdowns, sliders, caixas de texto e seletores de cores. Suporta personalização de cores, tamanhos de botões, efeitos de glassmorphism e interações otimizadas para dispositivos móveis.

---

## Instalação
1. Copie o código da biblioteca redzlib fornecido anteriormente.
2. Cole-o em um script Lua no Roblox Studio (por exemplo, em um `LocalScript` dentro de `StarterPlayerScripts`).
3. Certifique-se de que o script tenha acesso ao `CoreGui` para renderizar a interface.

```lua
local redzlib = loadstring(game:HttpGet("URL_DA_BIBLIOTECA"))() -- Se hospedado online
-- ou
local redzlib = require(game.ReplicatedStorage.redzlib) -- Se local
```

---

## Criação de uma Janela
Para começar, crie uma janela principal com o método `MakeWindow`. Este método aceita configurações como título, subtítulo, tamanho e tema.

```lua
local Window = redzlib:MakeWindow({
    Title = "Minha Interface",
    SubTitle = "Bem-vindo!",
    Size = UDim2.fromOffset(600, 400),
    Theme = "Amoled" -- Darker, Dark, Purple, Amoled
})
```

### Parâmetros de MakeWindow
| Parâmetro | Tipo | Descrição | Padrão |
|-----------|------|-----------|--------|
| Title | string | Título da janela | "redz Hub" |
| SubTitle | string | Subtítulo da janela | "" |
| Size | UDim2 | Tamanho da janela | UDim2.fromOffset(550, 380) |
| Theme | string | Tema visual | "Darker" |

---

## Métodos Disponíveis

### Janela (Window)
A janela é o contêiner principal da interface. Métodos disponíveis:

- **CloseBtn()**: Fecha a janela.
  ```lua
  Window:CloseBtn()
  ```

- **MinimizeBtn()**: Minimiza ou restaura a janela.
  ```lua
  Window:MinimizeBtn()
  ```

- **Minimize()**: Alterna a visibilidade da janela.
  ```lua
  Window:Minimize()
  ```

- **AddMinimizeButton(Configs)**: Adiciona um botão de minimizar flutuante.
  ```lua
  Window:AddMinimizeButton({
      Button = { Image = "rbxassetid://10734924532" },
      Corner = UDim.new(0, 8)
  })
  ```

- **Set(Title, SubTitle)**: Define título e/ou subtítulo.
  ```lua
  Window:Set("Novo Título", "Novo Subtítulo")
  ```

- **Dialog(Configs)**: Cria uma caixa de diálogo com botões.
  ```lua
  local Dialog = Window:Dialog({
      Title = "Confirmação",
      Text = "Deseja continuar?",
      Options = {
          { Name = "Sim", Callback = function() print("Confirmado!") end },
          { Name = "Não", Callback = function() print("Cancelado!") end }
      }
  })
  Dialog:Close() -- Fecha o diálogo
  ```

- **SelectTab(Tab)**: Seleciona uma aba específica por índice ou objeto.
  ```lua
  Window:SelectTab(1) -- Seleciona a primeira aba
  ```

- **MakeTab(Configs)**: Cria uma nova aba.
  ```lua
  local Tab = Window:MakeTab({
      Title = "Aba Principal",
      Icon = "home"
  })
  ```

### Aba (Tab)
Cada aba contém elementos como seções, botões, etc. Métodos disponíveis:

- **Enable()**: Ativa a aba.
  ```lua
  Tab:Enable()
  ```

- **Disable()**: Desativa a aba.
  ```lua
  Tab:Disable()
  ```

- **Visible(Bool)**: Define a visibilidade da aba.
  ```lua
  Tab:Visible(false) -- Esconde a aba
  ```

- **Destroy()**: Remove a aba.
  ```lua
  Tab:Destroy()
  ```

- **AddSection(Configs)**: Adiciona uma seção com cor personalizável.
  ```lua
  local Section = Tab:AddSection({
      Name = "Minha Seção",
      Color = Color3.fromRGB(255, 0, 0) -- Vermelho
  })
  ```

### Seção (Section)
- **Visible(Bool)**: Define a visibilidade da seção.
  ```lua
  Section:Visible(false)
  ```

- **Destroy()**: Remove a seção.
  ```lua
  Section:Destroy()
  ```

- **Set(Name)**: Altera o nome da seção.
  ```lua
  Section:Set("Nova Seção")
  ```

### Parágrafo (Paragraph)
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  Paragraph:Visible(false)
  ```

- **Destroy()**: Remove o parágrafo.
  ```lua
  Paragraph:Destroy()
  ```

- **SetTitle(Title)**: Altera o título.
  ```lua
  Paragraph:SetTitle("Novo Título")
  ```

- **SetDesc(Description)**: Altera a descrição.
  ```lua
  Paragraph:SetDesc("Nova descrição")
  ```

- **Set(Title, Description)**: Altera título e descrição.
  ```lua
  Paragraph:Set("Título", "Descrição")
  ```

### Botão (Button)
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  Button:Visible(false)
  ```

- **Destroy()**: Remove o botão.
  ```lua
  Button:Destroy()
  ```

- **Callback(Func)**: Define ou atualiza a função de callback.
  ```lua
  Button:Callback(function() print("Novo clique!") end)
  ```

- **Set(Title, Description)**: Altera título e/ou descrição.
  ```lua
  Button:Set("Novo Botão", "Nova descrição")
  ```

### Toggle
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  Toggle:Visible(false)
  ```

- **Destroy()**: Remove o toggle.
  ```lua
  Toggle:Destroy()
  ```

- **Callback(Func)**: Define ou atualiza o callback.
  ```lua
  Toggle:Callback(function(value) print("Toggle:", value) end)
  ```

- **Set(Value)**: Define o estado (true/false) ou título/descrição.
  ```lua
  Toggle:Set(true) -- Ativa o toggle
  Toggle:Set("Novo Toggle", "Nova descrição")
  ```

### Dropdown
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  Dropdown:Visible(false)
  ```

- **Destroy()**: Remove o dropdown.
  ```lua
  Dropdown:Destroy()
  ```

- **Callback(Func)**: Define ou atualiza o callback.
  ```lua
  Dropdown:Callback(function(selected) print("Selecionado:", selected) end)
  ```

- **Add(Options)**: Adiciona novas opções.
  ```lua
  Dropdown:Add({"Opção 3", "Opção 4"})
  ```

- **Remove(Option)**: Remove uma opção pelo nome ou índice.
  ```lua
  Dropdown:Remove("Opção 1")
  ```

- **Select(Option)**: Seleciona uma opção pelo nome ou índice.
  ```lua
  Dropdown:Select("Opção 2")
  ```

- **Set(Options, Clear)**: Atualiza a lista de opções (Clear = true limpa as opções atuais).
  ```lua
  Dropdown:Set({"Nova Opção 1", "Nova Opção 2"}, true)
  ```

### Slider
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  Slider:Visible(false)
  ```

- **Destroy()**: Remove o slider.
  ```lua
  Slider:Destroy()
  ```

- **Callback(Func)**: Define ou atualiza o callback.
  ```lua
  Slider:Callback(function(value) print("Valor:", value) end)
  ```

- **Set(Value)**: Define o valor do slider ou título/descrição.
  ```lua
  Slider:Set(50) -- Define valor 50
  Slider:Set("Novo Slider", "Nova descrição")
  ```

### Caixa de Texto (TextBox)
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  TextBox:Visible(false)
  ```

- **Destroy()**: Remove a caixa de texto.
  ```lua
  TextBox:Destroy()
  ```

- **OnChanging(Func)**: Define uma função para manipular o texto durante a digitação.
  ```lua
  TextBox.OnChanging = function(text) return text:upper() end
  ```

### Convite do Discord
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  DiscordInvite:Visible(false)
  ```

- **Destroy()**: Remove o convite.
  ```lua
  DiscordInvite:Destroy()
  ```

### Seletor de Cores (ColorPicker)
- **Visible(Bool)**: Define a visibilidade.
  ```lua
  ColorPicker:Visible(false)
  ```

- **Destroy()**: Remove o seletor de cores.
  ```lua
  ColorPicker:Destroy()
  ```

- **Callback(Func)**: Define ou atualiza o callback.
  ```lua
  ColorPicker:Callback(function(color) print("Cor:", color) end)
  ```

- **Set(Color)**: Define a cor selecionada.
  ```lua
  ColorPicker:Set(Color3.fromRGB(0, 255, 0)) -- Verde
  ```

---

## Atualização de Elementos

### Atualizar Dropdowns
Os dropdowns podem ser atualizados dinamicamente usando os métodos `Add`, `Remove` e `Set`.

- **Adicionar Opções**:
  ```lua
  Dropdown:Add("Nova Opção")
  Dropdown:Add({"Opção A", "Opção B"})
  ```

- **Remover Opções**:
  ```lua
  Dropdown:Remove("Opção A") -- Remove pelo nome
  Dropdown:Remove(1) -- Remove pelo índice
  ```

- **Substituir Opções**:
  ```lua
  Dropdown:Set({"Opção 1", "Opção 2", "Opção 3"}, true) -- Substitui todas as opções
  Dropdown:Set({"Opção Extra"}, false) -- Adiciona sem limpar
  ```

- **Selecionar uma Opção**:
  ```lua
  Dropdown:Select("Opção 2") -- Seleciona pelo nome
  Dropdown:Select(2) -- Seleciona pelo índice
  ```

---

## Exemplo Completo
```lua
local redzlib = require(game.ReplicatedStorage.redzlib) -- Substitua pelo caminho correto

-- Criar janela
local Window = redzlib:MakeWindow({
    Title = "Minha Interface",
    SubTitle = "Teste de UI",
    Size = UDim2.fromOffset(600, 400),
    Theme = "Amoled"
})

-- Criar aba
local Tab = Window:MakeTab({
    Title = "Configurações",
    Icon = "settings"
})

-- Adicionar seção
local Section = Tab:AddSection({
    Name = "Controles",
    Color = Color3.fromRGB(200, 0, 0) -- Vermelho
})

-- Adicionar botão com tamanho personalizado
local Button = Tab:AddButton({
    Name = "Ativar Algo",
    Desc = "Clique para ativar a função",
    Size = UDim2.new(0.5, -20), -- Tamanho reduzido
    Callback = function() print("Botão clicado!") end
})

-- Adicionar toggle
local Toggle = Tab:AddToggle({
    Name = "Modo Noturno",
    Default = true,
    Flag = "NightMode",
    Callback = function(value) print("Modo Noturno:", value) end
})

-- Adicionar dropdown
local Dropdown = Tab:AddDropdown({
    Name = "Seleção de Modo",
    Options = {"Fácil", "Médio", "Difícil"},
    Default = "Médio",
    Flag = "GameMode",
    Callback = function(selected) print("Modo selecionado:", selected) end
})

-- Adicionar slider
local Slider = Tab:AddSlider({
    Name = "Volume",
    Min = 0,
    Max = 100,
    Increase = 1,
    Default = 50,
    Flag = "VolumeLevel",
    Callback = function(value) print("Volume:", value) end
})

-- Adicionar caixa de texto
local TextBox = Tab:AddTextBox({
    Name = "Nome do Jogador",
    Default = "Jogador1",
    PlaceholderText = "Digite seu nome",
    ClearText = true,
    Callback = function(text) print("Nome:", text) end
})

-- Adicionar convite do Discord
local DiscordInvite = Tab:AddDiscordInvite({
    Name = "Junte-se ao Discord",
    Desc = "Entre no nosso servidor!",
    Logo = "rbxassetid://10734962339",
    Invite = "https://discord.gg/exemplo"
})

-- Adicionar seletor de cores
local ColorPicker = Tab:AddColorPicker({
    Name = "Cor de Fundo",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(color) print("Cor selecionada:", color) end
})

-- Atualizar dropdown dinamicamente
task.spawn(function()
    task.wait(5)
    Dropdown:Set({"Muito Fácil", "Muito Difícil"}, true) -- Substitui opções
    Dropdown:Select("Muito Difícil") -- Seleciona nova opção
end)
```

---

## Notas Finais
- **Temas**: Use `Theme` para alternar entre "Darker", "Dark", "Purple" ou "Amoled". O tema Amoled suporta glassmorphism com transparência ajustável.
- **Flags**: Use flags para salvar estados (ex.: `Flag = "nome"`). Eles persistem em `redzlib.Flags`.
- **Mobile**: O seletor de cores e outros elementos são compatíveis com dispositivos móveis (toque).
- **Ícones**: Use ícones da biblioteca Lucide (ex.: "home", "settings") com `redzlib:GetIcon("nome")`.
- **Personalização**: Ajuste tamanhos de botões com `Size` e cores de seções com `Color`.

Para mais detalhes, consulte o código-fonte da biblioteca ou experimente os métodos no Roblox Studio.
