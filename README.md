# Chameleon

Este projeto é um sistema de design desenvolvido para permitir a estilização flexível e abrangente de componentes de interface do usuário. O objetivo é fornecer uma biblioteca de estilos que possa ser aplicada a diversos componentes, garantindo consistência visual e facilitando a manutenção do design em projetos de software.

## Estrutura de Pastas

/raiz
```plaintext
|-- /lib # Código fonte dos estilos e componentes
| |-- /themes # Temas aplicáveis aos componentes
| |  |-- /inheriteds # componentes baseados em outros componentes
| |  |-- /example_theme # tema exemplo extendido do tema base com componentes customizados
```

## Uso
Após a instalação do pacote, é possível importar os estilos e componentes diretamente no código fonte do projeto. Para isso, basta importar o arquivo principal do pacote e utilizar os componentes disponíveis.

### Iniciar o sistema de design
```dart
import 'package:flutter/material.dart';
import 'package:chameleon/chameleon.dart';

void main() {
// Inicialize o sistema de design com o tema base
  startDs(ChameleonBaseTheme());
  runApp(const MyApp());
}
```

### Utilizar um componente
```dart
class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key});

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        // Use o componente ChameleonText
      body: Center(child: ChameleonText(text: 'Texto',),),
    );
  }
}
```

## Criar um tema personalizado
```dart
import 'package:chameleon/chameleon.dart';
// O CustomTheme deve extender o ChameleonBaseTheme
class CustomTheme extends ChameleonBaseTheme {
}
```

### Crie um componente personalizado e adicione ao tema
```dart
import 'package:chameleon/chameleon.dart';

class CustomThemeTextComponent extends StatelessWidget implements TextWidgetChameleonType{
  const CustomThemeTextComponent({super.key});

  @override
  Widget build(BuildContext context) {
    final inheritedWidget = of(context);
    
    return  Text(inheritedWidget.text);
  }
}

class CustomTheme extends ChameleonBaseTheme {
    @override
    TextWidgetChameleonType get text => const CustomThemeTextComponent();
}
```

### Iniciar o sistema de design com o tema personalizado
```dart
import 'package:flutter/material.dart';
import 'package:chameleon/chameleon.dart';

void main() {
// Inicialize o sistema de design com o tema base
  startDs(CustomTheme());
  runApp(const MyApp());
}
```

## Rodar script para geração de tokens do Design
para rodar o script de geração de tokens do design, é importante que o arquivo de tokens esteja na pasta `assets/design_tokens/design_token.json`:

```bash
flutter pub run chameleon:tokens_generate
```

caso queria alterar o caminho do arquivo de tokens, é possível passar o caminho como argumento:

```bash
flutter pub run chameleon:tokens_generate --path=design_token.json
```

é importante que o arquivo de tokens esteja no formato json, com a seguinte estrutura:

```json
{
  "figmaScale": 1.045,
  "colors": {
    "light": {
      "primary": "#FF0000",
      "secondary": "#00FF00",
      "background": "#FFFFFF",
      "text": "#000000"
    },
  },
  "typography": {
    "subtitle": {
      "fontFamily": "Roboto",
      "fontSize": 16,
      "fontWeight": 400,
      "letterSpacing": 0.5,
      "lineHeight": 1.5
    },
  }
}
```
