# Site

[Clique aqui para visitar o site "Escalas Match"](https://sites.google.com/view/criscleiescalas)

# Escalas Match

Sistema web para gerenciamento de escalas de folgas com interface moderna e autenticação por token.

## Visão Geral

O Escalas Match é uma aplicação web desenvolvida para facilitar o gerenciamento e visualização de escalas de trabalho, permitindo que usuários autorizados cadastrem, editem e visualizem folgas de diferentes pessoas em formato de calendário mensal.

## Funcionalidades

### 🔐 Autenticação
- Sistema de acesso por token
- Validação via Appwrite Functions
- Interface de login com feedback visual
- Ocultação automática do conteúdo principal até autenticação

### 📅 Gerenciamento de Escalas
- Visualização em calendário mensal
- Cadastro de folgas por pessoa
- Edição de escalas existentes
- Exclusão de escalas
- Seleção automática do mês atual
- Navegação entre diferentes meses/anos

### 👥 Gestão de Pessoas
- Sistema dinâmico baseado nos dados do banco
- Identificação visual por cores diferentes
- Suporte a múltiplas pessoas (Cris, Clei, etc.)

### 🎨 Interface Moderna
- Design responsivo com gradientes e efeitos visuais
- Tema escuro com elementos glassmorphism
- Animações e transições suaves
- Compatibilidade mobile
- Notificações visuais integradas

## Tecnologias Utilizadas

### Frontend
- **HTML5** - Estrutura semântica
- **CSS3** - Estilização avançada com:
  - Gradients e backdrop-filter
  - Flexbox e Grid
  - Media queries para responsividade
  - Animações CSS
- **JavaScript ES6+** - Lógica da aplicação:
  - Módulos ES6
  - Promises e async/await
  - Manipulação DOM moderna
  - Event handling

### Backend/Serviços
- **Appwrite** - Backend-as-a-Service:
  - Database para armazenamento de escalas
  - Functions para validação de tokens
  - Client SDK para integração
- **CDN** - Carregamento de dependências externas

## Estrutura do Projeto

```
escalas-match/
├── index.html                 # Arquivo principal
├── README.md                  # Este arquivo
└── assets/                    # Recursos externos (CDN)
    ├── notification-new.svg
    └── counter-new.svg
```

## Configuração do Banco de Dados

### Coleção: `escalas`
```json
{
  "people": "string",      // Nome da pessoa
  "year": "integer",       // Ano da escala
  "month": "string",       // Nome do mês em português
  "daysOff": "array"       // Array de dias de folga (números)
}
```

### Índices Recomendados
- `people` + `year` + `month` (único)
- `year` (para consultas por ano)
- `month` (para consultas por mês)

## Configuração do Appwrite

### Variáveis de Ambiente
```javascript
const DATABASE_ID = '686a68130002b51fced0';
const COLLECTION_ID = '68c535f2001de9505bde';
const FUNCTION_ID = '68c5be1b00315ff07f89';
const PROJECT_ID = '686a67d5003a1b4b1bf9';
const ENDPOINT = 'https://nyc.cloud.appwrite.io/v1';
```

### Função de Validação de Token
A aplicação utiliza uma Appwrite Function para validar tokens de acesso. A função deve:
- Receber um JSON com o token: `{"token": "valor_do_token"}`
- Retornar: `{"success": true/false}`

## Como Usar

### 1. Acesso Inicial
1. Abra a aplicação no navegador
2. Digite o token de acesso válido
3. Clique em "Acessar"
4. Aguarde a validação e liberação do conteúdo

### 2. Visualização de Escalas
- O calendário carrega automaticamente o mês atual (se disponível)
- Use o seletor de mês/ano para navegar
- Folgas são identificadas por cores:
  - Rosa: Folgas da Cris
  - Azul: Folgas do Clei

### 3. Edição de Escalas
1. Clique em "Editar Folgas"
2. Selecione a pessoa e período
3. Marque os dias de folga no calendário
4. Salve as alterações

### 4. Exclusão de Escalas
1. No modal de edição, selecione pessoa, mês e ano
2. Clique no link "Excluir escala"
3. Confirme a exclusão

## Estrutura do Código

### Organização Modular
```javascript
// Inicialização do Appwrite
function initAppwrite() { ... }

// Operações CRUD
async function saveScheduleAppwrite() { ... }
async function deleteScheduleAppwrite() { ... }

// Geração de Interface
async function loadAvailableMonthsYears() { ... }
async function buildCalendar() { ... }

// Editor de Folgas (Module Pattern)
const FolgasEditor = (() => {
  // Estado e elementos privados
  // Funções públicas expostas
})();

// Autenticação (ES6 Modules)
import { Client, Functions } from 'appwrite';
```

### Padrões Utilizados
- **Module Pattern** - Encapsulamento do editor
- **ES6 Modules** - Importação de dependências
- **Async/Await** - Operações assíncronas
- **Event Delegation** - Gerenciamento de eventos
- **Responsive Design** - Interface adaptativa

## Recursos de Acessibilidade

- Contraste adequado entre cores
- Navegação por teclado
- Labels semânticos
- Mensagens de feedback claras
- Responsividade em diferentes dispositivos

## Compatibilidade

### Navegadores Suportados
- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

### Dispositivos
- Desktop (1024px+)
- Tablet (768px-1023px)
- Mobile (320px-767px)

## Performance

### Otimizações Implementadas
- Carregamento assíncrono de dependências
- Cache de elementos DOM
- Lazy loading de dados
- Debounce em eventos de input
- Minimização de redraws

## Segurança

### Medidas Implementadas
- Validação de token no servidor
- Ocultação de conteúdo até autenticação
- Sanitização de inputs
- Validação de dados no cliente e servidor
- Uso de HTTPS obrigatório

## Manutenção

### Logs e Debug
```javascript
console.log('Dados carregados:', response.documents);
console.error('Erro ao salvar:', error);
```

### Monitoramento
- Verificação de conectividade com Appwrite
- Fallbacks para falhas de conexão
- Mensagens de erro user-friendly

## Troubleshooting

### Problemas Comuns

**Token inválido**
- Verificar se o token está correto
- Confirmar configuração da função Appwrite
- Verificar logs do servidor

**Dados não carregam**
- Verificar conexão com internet
- Confirmar configurações do banco
- Verificar permissões do projeto Appwrite

**Interface não responsiva**
- Limpar cache do navegador
- Verificar compatibilidade do navegador
- Testar em modo anônimo

## Contribuição

### Padrões de Código
- Indentação: 2 espaços
- Nomenclatura: camelCase para JS, kebab-case para CSS
- Comentários: em português para lógica de negócio
- Commits: convenção conventional commits

### Estrutura de Commits
```
feat: adiciona nova funcionalidade
fix: corrige bug específico
style: ajustes de CSS/UI
refactor: reestruturação de código
docs: atualização de documentação
```

## Roadmap

### Próximas Funcionalidades
- [ ] Exportação para PDF
- [ ] Notificações por email
- [ ] Histórico de alterações
- [ ] Backup automático
- [ ] Tema claro/escuro
- [ ] PWA (Progressive Web App)

### Melhorias Técnicas
- [ ] Testes automatizados
- [ ] Webpack/Vite para build
- [ ] TypeScript migration
- [ ] Service Workers
- [ ] Offline support

## Suporte

Para suporte técnico ou dúvidas sobre o sistema, entre em contato através dos canais apropriados da organização.

## Licença

Este projeto é de uso interno e proprietário. Todos os direitos reservados.
