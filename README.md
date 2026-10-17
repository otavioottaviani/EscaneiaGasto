# 📸 EscaneiaGasto

Site que lê comprovantes automaticamente e calcula seus gastos. Basta enviar a foto do comprovante: a IA identifica o estabelecimento, os itens e os valores, e o site soma o total gasto, sem digitar nada.

## Como funciona

1. Você toca em **"Toque para fotografar o comprovante"** e escolhe uma foto ou imagem.
2. A imagem é enviada para uma IA de visão através do [Puter.js](https://developer.puter.com/) (`puter.ai.chat`), junto com um prompt que pede uma resposta em formato fixo.
3. A IA responde em uma linha com duas partes separadas por `|`:
   - **Parte 1:** emoji da categoria, nome do estabelecimento e a lista de itens com valores.
   - **Parte 2:** o total pago, apenas o número.
4. O `scripts.js` separa as duas partes, mostra o comprovante na lista e soma o total ao **Total gasto** no topo da página.
5. Cada nova foto é adicionada à lista e o total acumulado é atualizado.

### Categorias reconhecidas

| Emoji | Categoria |
|-------|-----------|
| 🛒 | Mercado |
| 🚗 | Transporte |
| 🍔 | Comida |
| 💊 | Saúde |
| 🎉 | Lazer |
| 🏠 | Casa |
| 💸 | Outros |

## ⚠️ Conexão com o Puter (necessária)

A leitura das imagens depende do **Puter.js**, carregado no `index.html`:

```html
<script src="https://js.puter.com/v2/"></script>
```

Para a IA funcionar:

- Ao enviar o primeiro comprovante, o Puter abre uma janela pedindo para você **entrar ou criar uma conta gratuita no Puter**. É preciso fazer esse login/conexão para a IA responder.
- Se o navegador bloquear pop-ups, **permita pop-ups** para o site, senão a janela de login não aparece e nada acontece.
- É necessário ter **conexão com a internet**, pois a análise é feita pela IA do Puter.
- Não há chave de API no código: o uso da IA é cobrado do usuário no próprio Puter (modelo "user pays"), então o projeto não precisa de backend nem de credenciais.

## Como rodar

1. Clone o repositório:
   ```bash
   git clone https://github.com/otavioottaviani/EscaneiaGasto.git
   ```
2. Abra o `index.html` no navegador. Para evitar bloqueios do navegador, o ideal é servir a pasta localmente, por exemplo com a extensão **Live Server** do VS Code ou:
   ```bash
   python -m http.server 8000
   ```
   e acessar `http://localhost:8000`.
3. Clique para enviar a foto de um comprovante e faça login no Puter quando a janela aparecer.

## Tecnologias

- HTML5
- CSS3
- JavaScript
- [Puter.js](https://developer.puter.com/) (IA de visão via `puter.ai.chat`)

## Estrutura

```
EscaneiaGasto/
├── index.html    # estrutura da página e carregamento do Puter.js
├── scripts.js    # envia a foto à IA, trata a resposta e soma o total
└── style.css     # estilos da interface
```

## Limitações

- A precisão depende da qualidade da foto (boa iluminação e comprovante legível).
- O formato da resposta da IA é controlado pelo prompt; se ela responder fora do padrão, a leitura daquela nota pode falhar.
- Os dados ficam apenas na página aberta: ao recarregar, a lista e o total são zerados.

## Autor

Feito por [Otávio Ottaviani](https://github.com/otavioottaviani).
