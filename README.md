# redz Hub v2 - Biblioteca UI para Roblox Exploits

[![GitHub stars](https://img.shields.io/github/stars/TERCEIRO-COMANDO-DA-CAPITAL/hubV2?style=social)](https://github.com/TERCEIRO-COMANDO-DA-CAPITAL/hubV2) [![GitHub forks](https://img.shields.io/github/forks/TERCEIRO-COMANDO-DA-CAPITAL/hubV2?style=social)](https://github.com/TERCEIRO-COMANDO-DA-CAPITAL/hubV2) [![GitHub license](https://img.shields.io/github/license/TERCEIRO-COMANDO-DA-CAPITAL/hubV2)](https://github.com/TERCEIRO-COMANDO-DA-CAPITAL/hubV2)

## Visão Geral
O **redz Hub v2** é uma biblioteca Lua avançada para criar interfaces gráficas (GUIs) modernas e responsivas no Roblox, otimizada para exploits e scripts de automação. Inspirada em designs como glassmorphism e Amoled, ela permite criar hubs de cheats, menus de configurações e painéis interativos com animações suaves, suporte a mobile e personalizações fáceis.

### Recursos Principais
- **Temas Visuais**: Suporte a temas como Amoled (glassmorphism escuro com transparência), Darker, Dark e Purple, com acentos vermelhos para destaques (ex.: toggles ativos).
- **Elementos Interativos**: Botões com tamanhos ajustáveis, toggles com estados visuais, dropdowns atualizáveis dinamicamente, sliders, caixas de texto, seletores de cores (com suporte touch para mobile) e parágrafos informativos.
- **Estrutura Flexível**: Janelas, abas e seções organizadas, com diálogos modais e ícones Lucide.
- **Otimização para Exploits**: Leve, sem dependências externas, compatível com executores como Synapse X, Krnl, Fluxus e outros. Suporte a flags para salvar estados persistentes.
- **Efeitos Modernos**: Animações com TweenService, ripple effects em botões, sombras simuladas e gradientes para um visual premium.
- **Compatibilidade**: Funciona em PC e mobile, com drag-and-drop e interações touch.

O hub é ideal para desenvolvedores de scripts Roblox que querem um menu profissional para features como aimbot, ESP, speed hacks, etc., sem complicações.

## Instalação
### Via Loadstring (Recomendado para Exploits)
Cole o seguinte código no seu executor de exploits (ex.: Synapse X, Krnl). Isso carrega a biblioteca diretamente do GitHub.

```lua
-- Loadstring para redz Hub v2
local redzlib = loadstring(game:HttpGet("https://raw.githubusercontent.com/TERCEIRO-COMANDO-DA-CAPITAL/hubV2/refs/heads/main/hubV2.txt"))()

-- Exemplo rápido: Criar uma janela básica
local Window = redzlib:MakeWindow({Title = "Meu Exploit Hub", Theme = "Amoled"})
local Tab = Window:MakeTab({Title = "Features", Icon = "settings"})

-- Adicione elementos aqui (veja o tutorial abaixo)
```

**Nota**: Certifique-se de que o executor suporte `loadstring` e `HttpGet`. Se o link falhar, verifique a conexão ou baixe o arquivo manualmente.

### Via Download Manual
1. Acesse [hubV2.txt](https://raw.githubusercontent.com/TERCEIRO-COMANDO-DA-CAPITAL/hubV2/refs/heads/main/hubV2.txt) e copie o conteúdo.
2. Cole em um arquivo `.lua` e execute no seu exploit.
3. Ou clone o repositório: `git clone https://github.com/TERCEIRO-COMANDO-DA-CAPITAL/hubV2.git`.

## Tutorial de Uso
Este tutorial mostra como construir um hub completo passo a passo. Começamos com o **modelo básico do hub** (estrutura geral), e depois detalhamos os **métodos de uso para cada elemento**.

### 1. Modelo Básico do Hub
O hub segue uma estrutura hierárquica: **Janela** > **Aba** > **Seção** > **Elementos** (botões, toggles, etc.). Aqui vai um exemplo de modelo inicial para um exploit simples (ex.: menu de hacks).

```lua
-- Carregamento da biblioteca
local redzlib = loadstring(game:HttpGet("https://raw.githubusercontent.com/TERCEIRO-COMANDO-DA-CAPITAL/hubV2/refs/heads/main/hubV2.txt"))()

-- 1. Criar a Janela Principal (contêiner raiz)
local Window = redzlib:MakeWindow({
    Title = "redz Exploit Hub v2",  -- Título da janela
    SubTitle = "Feito para cheats avançados",  -- Subtítulo opcional
    Size = UDim2.fromOffset(550, 400),  -- Tamanho personalizado
    Theme = "Amoled"  -- Tema (Amoled para glassmorphism escuro com red accents)
})

-- 2. Criar uma Aba (página dentro da janela)
local Tab = Window:MakeTab({
    Title = "Combat Hacks",  -- Nome da aba
    Icon = "sword"  -- Ícone Lucide (opcional, ex.: "sword" para combate)
})

-- 3. Adicionar uma Seção (agrupador de elementos na aba)
local Section = Tab:AddSection({
    Name = "Aimbot Settings",  -- Nome da seção
    Color = Color3.fromRGB(200, 0, 0)  -- Cor personalizada (vermelho para destaque)
})

-- 4. Adicionar Elementos na Seção (exemplos básicos)
local Toggle = Tab:AddToggle({  -- Toggle para ativar aimbot
    Name = "Aimbot",
    Desc = "Ativa o aimbot automático",
    Default = false,  -- Estado inicial
    Flag = "AimbotEnabled",  -- Flag para salvar estado
    Callback = function(enabled)  -- Função executada ao mudar
        if enabled then
            -- Código do aimbot aqui (ex.: spawn thread para hack)
            print("Aimbot ativado!")
        else
            print("Aimbot desativado!")
        end
    end
})

local Slider = Tab:AddSlider({  -- Slider para sensibilidade
    Name = "Sensibilidade",
    Desc = "Ajusta a precisão do aimbot",
    Min = 0,  -- Valor mínimo
    Max = 100,  -- Valor máximo
    Increase = 1,  -- Incremento
    Default = 50,  -- Valor inicial
    Flag = "AimbotSens",  -- Flag para salvar
    Callback = function(value)
        -- Aplique o valor ao hack aqui
        print("Sensibilidade:", value)
    end
})

-- 5. Adicionar Outro Elemento (ex.: Dropdown para alvos)
local Dropdown = Tab:AddDropdown({
    Name = "Alvo Prioritário",
    Desc = "Escolha o tipo de inimigo",
    Options = {"Jogadores", "NPCs", "Todos"},  -- Opções iniciais
    Default = "Jogadores",  -- Seleção inicial
    MultiSelect = false,  -- Permitir múltipla seleção? (false por padrão)
    Flag = "TargetType",  -- Flag para salvar
    Callback = function(selected)
        -- Aplique a seleção ao hack
        print("Alvo:", selected)
    end
})

-- 6. Finalizar: O hub abre automaticamente. Use Window:CloseBtn() para fechar.
```

**Saída Esperada**: Uma janela escura com glassmorphism abre, mostrando a aba "Combat Hacks" com seção vermelha contendo toggle, slider e dropdown. Interaja para testar callbacks.

Agora, vamos aos **métodos detalhados para cada elemento**.

### 2. Métodos de Uso por Elemento
Cada elemento é adicionado a uma aba (`Tab`). Eles retornam um objeto com métodos para manipulação (ex.: esconder, atualizar). Use flags para persistência (ex.: `Flag = "meuFlag"` salva em `redzlib.Flags`).

#### Janela (Window) - Métodos Globais
- **MakeWindow(Configs)**: Cria a janela raiz.
  - Configs: `{Title, SubTitle, Size, Theme, Save}`.
- **CloseBtn()**: Fecha a janela.
- **MinimizeBtn()**: Minimiza/restaura.
- **Minimize()**: Alterna visibilidade.
- **Set(Title, SubTitle)**: Atualiza título/subtítulo.
- **Dialog(Configs)**: Mostra diálogo modal.
  - Ex.: `{Title = "Alerta", Text = "Hack ativado!", Options = {{Name = "OK", Callback = function() end}}}`.
- **SelectTab(Tab ou Index)**: Muda para aba específica.
- **MakeTab(Configs)**: Cria aba.
  - Configs: `{Title, Icon}` (Icon = nome Lucide, ex.: "cog").

#### Seção (Section) - Agrupador
- **AddSection(Configs)**: Adiciona seção.
  - Configs: `{Name, Color}` (Color = Color3 para título).
- **Visible(Bool)**: Mostra/esconde seção.
- **Set(Name)**: Atualiza nome.
- **Destroy()**: Remove seção.

#### Parágrafo (Paragraph) - Texto Informativo
- **AddParagraph(Configs)**: Adiciona texto.
  - Configs: `{Title, Text}`.
- **Set(Title, Text)**: Atualiza texto.
- **SetTitle(Title)** / **SetDesc(Text)**: Atualiza partes específicas.
- **Visible(Bool)** / **Destroy()**: Controle básico.

#### Botão (Button) - Ação Simples
- **AddButton(Configs)**: Adiciona botão.
  - Configs: `{Name, Desc, Size (UDim2), Callback (function)}`.
- **Callback(Func)**: Atualiza função de clique.
- **Set(Name, Desc)**: Atualiza texto.
- **Visible(Bool)** / **Destroy()**: Controle.

#### Toggle - Interruptor On/Off
- **AddToggle(Configs)**: Adiciona toggle.
  - Configs: `{Name, Desc, Default (bool), Flag (string), Callback (function(bool))}`.
- **Set(Value (bool))** ou **Set(Name, Desc)**: Altera estado ou texto.
- **Callback(Func)**: Atualiza função.
- **Visible(Bool)** / **Destroy()**: Controle.

#### Dropdown - Lista de Opções
- **AddDropdown(Configs)**: Adiciona dropdown.
  - Configs: `{Name, Desc, Options (table), Default, MultiSelect (bool), Flag, Callback (function(selected))}`.
- **Add(Options (table ou strings))**: Adiciona opções.
- **Remove(Option (string ou int))**: Remove por nome/índice.
- **Select(Option (string ou int))**: Seleciona opção.
- **Set(NewOptions (table), Clear (bool))**: Atualiza lista (Clear limpa antigas).
- **Callback(Func)** / **Visible(Bool)** / **Destroy()**: Controle.

#### Slider - Barra Deslizante
- **AddSlider(Configs)**: Adiciona slider.
  - Configs: `{Name, Desc, Min (num), Max (num), Increase (num), Default (num), Flag, Callback (function(num))}`.
- **Set(Value (num))** ou **Set(Name, Desc)**: Altera valor ou texto.
- **Callback(Func)** / **Visible(Bool)** / **Destroy()**: Controle.

#### Caixa de Texto (TextBox) - Input
- **AddTextBox(Configs)**: Adiciona input.
  - Configs: `{Name, Desc, Default (string), PlaceholderText, ClearText (bool), Callback (function(text))}`.
- **OnChanging = Func**: Manipula texto em tempo real (ex.: uppercase).
- **Visible(Bool)** / **Destroy()**: Controle.

#### Convite do Discord
- **AddDiscordInvite(Configs)**: Adiciona botão de convite.
  - Configs: `{Name, Desc, Logo (rbxassetid), Invite (string)}`.
- **Visible(Bool)** / **Destroy()**: Controle.
- Clique copia o invite para clipboard.

#### Seletor de Cores (ColorPicker)
- **AddColorPicker(Configs)**: Adiciona picker HSV.
  - Configs: `{Name, Desc, Default (Color3), Callback (function(Color3))}`.
- **Set(Color3)**: Atualiza cor.
- **Callback(Func)** / **Visible(Bool)** / **Destroy()**: Controle.
- Suporte mobile: Use toque para arrastar no picker.

## Exemplos Avançados
- **Atualizar Dropdown Dinamicamente** (ex.: carregar opções de um jogo):
  ```lua
  local Dropdown = Tab:AddDropdown({Name = "Itens", Options = {}})

  -- Simule carregamento
  task.spawn(function()
      local newItems = {"Espada", "Escudo", "Poção"}  -- De um API ou loop
      Dropdown:Set(newItems, true)  -- Limpa e adiciona
      Dropdown:Select("Espada")
  end)
  ```

- **Flag Persistente em Toggle**:
  ```lua
  local isEnabled = redzlib.Flags["MyHack"] or false  -- Recupera flag
  Toggle:Set(isEnabled)  -- Aplica
  ```

## Contribuições
- Fork o repo e envie PRs para novas features (ex.: mais temas).
- Relate issues para bugs.

## Licença
MIT License - Use livremente, mas credite o autor.

## Suporte
- Discord: [Link do Servidor](https://discord.gg/exemplo)
- Issues no GitHub para dúvidas.
