# Feature ✨

**feat: Classe Base DomReadyComponent para Inicialização Segura Após o DOM**

## Visão Geral 📄🧐

A classe `DomReadyComponent` serve como base para todos os componentes que necessitam aguardar o carregamento completo do DOM antes de iniciar suas operações. Ela fornece um mecanismo confiável e reutilizável para garantir que a inicialização de componentes derivados aconteça no momento apropriado.

## Contexto 🌍
Em aplicações web modernas, é comum que várias operações dependam da completa disponibilidade dos elementos do DOM. `DomReadyComponent` abstrai a lógica de espera pelo evento `DOMContentLoaded`, permitindo que componentes derivados se concentrem na implementação de suas funcionalidades específicas sem se preocupar com o estado de carregamento do DOM.

## Motivação 💡
A necessidade de uma classe base como `DomReadyComponent` surge da complexidade e dos desafios associados à manipulação correta do ciclo de vida do carregamento de páginas web. Simplificar o processo de garantir que o DOM esteja pronto antes de executar código de inicialização aumenta a confiabilidade e a manutenibilidade do código.

## Cenário 
Imagine uma aplicação web que carrega conteúdo dinâmico e widgets interativos. Cada widget precisa interagir com o DOM para configurar eventos e exibir informações. `DomReadyComponent` garante que todos os widgets sejam inicializados apenas após o DOM estar completamente carregado, evitando erros de elementos não encontrados.

## Requisitos 📝
- A classe `DomReadyComponent` deve ser estendida por quaisquer componentes que realizem manipulações do DOM em sua inicialização.
- Nenhum método adicional é necessário para acionar a inicialização; o construtor da classe base cuida da lógica de verificação do estado do DOM.

## Testes 🧪
- [x] Testes locais confirmam que a inicialização do componente só ocorre após o `DOMContentLoaded`.
- [ ] Testes em servidor não aplicáveis.
- [ ] Testes de integração dependem da implementação específica dos componentes derivados.
- [ ] Testes de aceitação podem ser realizados em componentes derivados para validar a interação com o DOM.

## 🆕 Versão 🔢
- [x] Fase do projeto: Alfa
- [x] Versão da classe/código: 1.0.0
- [x] Linguagem: JavaScript

## 🛠️ Implementação da Classe

A `DomReadyComponent` abstrai a lógica de inicialização segura para componentes dependentes do DOM.

```javascript
/**
 * Classe base para garantir a inicialização de componentes após o DOM estar completamente carregado.
 * Esta classe foi projetada para ser estendida por outros componentes que precisam aguardar o carregamento do DOM
 * antes de executar sua lógica de inicialização.
 */
class DomReadyComponent {
    /**
     * Construtor da classe DomReadyComponent.
     * Verifica o estado atual do DOM e decide se inicializa imediatamente ou espera pelo evento DOMContentLoaded.
     */
    constructor() {
        /**
         * Indica se a inicialização foi concluída com sucesso.
         * @type {boolean}
         */
        this.initializedSuccessfully = false;

        if (document.readyState !== "loading") {
            // Se o DOM já estiver carregado, inicializa imediatamente.
            this.initialize();
        } else {
            // Caso contrário, aguarda o evento DOMContentLoaded para inicializar.
            document.addEventListener("DOMContentLoaded", () => {
                this.initialize();
            });
        }
    }

    /**
     * Método de inicialização chamado uma vez que o DOM está pronto.
     * Este método deve ser sobreescrito por classes derivadas para implementar lógica de inicialização específica.
     */
    initialize() {
        console.log("✅ Inicialização bem-sucedida!");
        this.initializedSuccessfully = true;
    }
}

```

Esta classe serve como um ponto de partida robusto para qualquer componente que necessite esperar pelo carregamento do DOM, simplificando a gestão do ciclo de vida de inicialização.


## Amostra genérica 📄🌐

Para utilizar a classe `InitializableComponent` como base para seus próprios componentes que necessitam de inicialização após o carregamento completo do DOM, você precisa estendê-la em suas próprias classes. Aqui está um exemplo genérico de como você pode fazer isso, criando um componente que interage com o DOM após estar completamente carregado:

### Passo 1: Definir a Classe `InitializableComponent`

```javascript
class InitializableComponent {
    constructor() {
        this.initializedSuccessfully = false;
        if (document.readyState !== "loading") {
            this.initialize();
        } else {
            document.addEventListener("DOMContentLoaded", () => {
                this.initialize();
            });
        }
    }

    initialize() {
        console.log("✅ Inicialização bem-sucedida!");
        this.initializedSuccessfully = true;
    }
}
```

### Passo 2: Criar uma Classe que Estende `InitializableComponent`

Imagine que você quer criar um componente chamado `DynamicBanner` que carrega um banner dinâmico na página. Este componente precisa esperar o DOM estar pronto para encontrar o elemento do banner e configurar seu conteúdo.

```javascript
class DynamicBanner extends InitializableComponent {
    constructor(bannerId, bannerContent) {
        super(); // Chama o construtor da classe base
        this.bannerId = bannerId;
        this.bannerContent = bannerContent;
    }

    initialize() {
        super.initialize(); // Garante que a lógica de inicialização da classe base seja executada
        this.setupBanner();
    }

    setupBanner() {
        const bannerElement = document.getElementById(this.bannerId);
        if (bannerElement) {
            bannerElement.innerHTML = this.bannerContent;
            console.log(`Banner #${this.bannerId} configurado com sucesso.`);
        } else {
            console.error(`Elemento do banner #${this.bannerId} não encontrado.`);
        }
    }
}
```

### Passo 3: Usar a Classe Derivada

Para usar a classe `DynamicBanner`, você simplesmente cria uma nova instância dela, passando o ID do elemento do banner e o conteúdo desejado como argumentos:

```javascript
const banner = new DynamicBanner('meuBanner', '<h1>Olá, Mundo!</h1><p>Este é um banner dinâmico.</p>');
```

Neste exemplo, a classe `DynamicBanner` estende `InitializableComponent` para garantir que sua lógica de inicialização específica (configurando o conteúdo do banner) só seja executada após o DOM estar completamente carregado. Isso é particularmente útil para componentes que dependem de elementos do DOM que podem não estar imediatamente disponíveis no momento da execução do script.