# Monitora PERT

**Painel de Acompanhamento dos Planos Táticos de Reocupação Territorial**

Este projeto é um MVP para apresentação à chefia, com:

- Google Sheets como repositório de dados;
- Google Apps Script como API e gerador de PDF;
- GitHub Pages como dashboard web;
- extração de relatório executivo em PDF.

## 1. Estrutura do projeto

```text
monitora-pert-github/
├── index.html
├── assets/
│   ├── css/
│   │   └── styles.css
│   └── js/
│       └── app.js
├── apps-script/
│   └── Code.gs
└── docs/
    └── estrutura_planilha.md
```

## 2. Fluxo do sistema

```text
Google Sheets
   ↓
Apps Script / Web App
   ↓
Dashboard no GitHub Pages
   ↓
Relatório PDF salvo no Google Drive
```

O GitHub hospeda somente a interface. Os dados ficam no Google Sheets.

## 3. Como configurar o Google Sheets

1. Crie uma planilha no Google Sheets.
2. Vá em **Extensões > Apps Script**.
3. Cole o conteúdo de `apps-script/Code.gs`.
4. Salve o projeto.
5. Execute a função `setup()` uma vez.
6. Autorize as permissões solicitadas.

A função `setup()` cria automaticamente as abas, cabeçalhos e dados demonstrativos.

## 4. Como publicar o Apps Script como API

1. No Apps Script, clique em **Implantar > Nova implantação**.
2. Escolha **App da Web**.
3. Em **Executar como**, selecione **Eu**.
4. Em **Quem pode acessar**, selecione a opção adequada ao ambiente:
   - `Qualquer pessoa com o link`, para demonstração;
   - domínio institucional, caso disponível;
   - acesso restrito, para ambiente interno.
5. Clique em **Implantar**.
6. Copie a URL final terminada em `/exec`.

## 5. Como vincular o dashboard ao Apps Script

Abra o arquivo:

```text
assets/js/app.js
```

Localize:

```javascript
const CONFIG = {
  API_URL: "",
  DEFAULT_PERIODO: ""
};
```

Cole a URL do Web App:

```javascript
const CONFIG = {
  API_URL: "https://script.google.com/macros/s/SEU_DEPLOY_ID/exec",
  DEFAULT_PERIODO: ""
};
```

Enquanto `API_URL` estiver vazia, o painel abre em modo demonstração.

## 6. Como colocar no GitHub Pages

1. Crie um repositório no GitHub.
2. Envie os arquivos deste projeto.
3. Vá em **Settings > Pages**.
4. Em **Build and deployment**, selecione:
   - Source: `Deploy from a branch`;
   - Branch: `main`;
   - Folder: `/root`.
5. Aguarde a publicação.
6. Abra a URL do GitHub Pages.

## 7. Como gerar relatório PDF

No dashboard, clique em **Gerar relatório PDF**.

- Com `API_URL` configurada, o Apps Script gera um PDF e salva no Google Drive.
- Sem `API_URL`, o painel usa o recurso de impressão do navegador, permitindo “Salvar como PDF”.

## 8. Abas da planilha

As abas principais são:

- `TERRITORIOS`
- `PLANOS_TATICOS`
- `EIXOS_ACOES`
- `PROJETOS`
- `INDICADORES`
- `COLETAS`
- `RISCOS`
- `PENDENCIAS`
- `DELIBERACOES`
- `EVIDENCIAS`
- `USUARIOS`
- `LOGS`

A aba mais importante é `PROJETOS`, pois cada projeto/iniciativa do Plano de Ação deve estar vinculado a um indicador de esforço.

## 9. Observação de segurança

Para apresentação, os dados de exemplo podem ser utilizados sem restrição.

Para uso institucional real, evite publicar dados sensíveis, operacionais, pessoais ou sigilosos em repositório público ou planilha com acesso aberto. O ideal é manter:

- GitHub apenas com a interface;
- dados no Google Sheets com permissão restrita;
- Web App do Apps Script limitado ao domínio institucional, sempre que possível.
