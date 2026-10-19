# Documentação Oficial: App de Treinos V10 & Desafio 21 Dias

> **Fonte da Verdade:** Este documento define as regras de negócio, a arquitetura offline-first e o guia operacional para o aplicativo de treinos de Fabbio.

---

## 1. Visão Geral do Produto

O aplicativo [APP_TREINO_V11.html](file:///d:/Treinos/app/APP_TREINO_V11.html) é uma aplicação web progressiva (PWA), desenvolvida em Vanilla HTML5/CSS3/JS, projetada para uso em smartphones dentro da academia ou em viagens, com suporte total a funcionamento offline.

O ecossistema é dividido em 3 módulos principais:
1. **🏋️ Treino V10 (Semanal):** Divisão Fullbody de alta sobrecarga progressiva, intercalada com Cardio Zona 2 para oxidação lipídica e HIIT 4×4 para elevação do VO₂ Máximo.
2. **🔥 Desafio 21 Dias (Método 40+ Seca Pochete):** 21 aulas em vídeo de alta densidade (13 a 23 minutos), com foco no *Boom Hormonal* (estímulo natural a GH e Testosterona), redução de gordura visceral teimosa e controle de conclusão.
3. **🥗 Dieta & Protocolo 40+:** Guia nutricional prático baseado no *Ebook Seca Pochete Masculino*, com divisão das 4 refeições diárias e tabela expansível de substituições equivalentes de alimentos.

---

## 2. Estrutura do Repositório

```text
d:\Treinos\
├── .gitignore               # Ignora arquivos de vídeo pesados (>100MB) e temporários
├── index.html               # Ponto de entrada raiz com redirecionamento automático
├── gemini.md                # Stack técnica, deploy e convenções do repositório
├── docs/
│   └── readme.md            # Este manual operacional e regras de negócio
├── app/
│   └── APP_TREINO_V11.html  # Aplicação completa (CSS, HTML e lógica JS unificados)
├── protocolos/              # Ebooks e diretrizes nutricionais originais em PDF
└── videos/                  # Os 21 arquivos MP4 originais (armazenados localmente)
```

---

## 3. Como Publicar no GitHub Pages (Atualização Automática a Cada Commit)

O GitHub Pages hospeda seu app gratuitamente com certificado de segurança (HTTPS).

### Passo 1: Subir o repositório para o seu GitHub
Abra o terminal e execute:
```bash
git add .
git commit -m "feat: lancamento v11 com desafio 21 dias e player offline"
git remote add origin https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git
git push -u origin main
```
*(Nota: O arquivo `.gitignore` já impede que a pasta `videos/` seja enviada, garantindo que o limite de 100 MB do GitHub nunca seja violado).*

### Passo 2: Ativar o GitHub Pages no Repositório
1. No seu repositório no GitHub, clique na aba **Settings** (Configurações).
2. No menu lateral esquerdo, clique em **Pages**.
3. Em **Build and deployment > Source**, selecione `Deploy from a branch`.
4. Em **Branch**, selecione `main` e a pasta `/(root)`. Clique em **Save**.
5. Em cerca de 1 a 2 minutos, o GitHub exibirá o link oficial do seu app:
   `https://SEU_USUARIO.github.io/SEU_REPOSITORIO/`

Pronto! Sempre que você fizer uma alteração e der `git push`, o GitHub Pages atualiza o app no seu celular automaticamente.

---

## 4. Guia de Armazenamento e Vinculação dos Vídeos no Celular

### 4.1. Entendendo a Segurança Web (Por que caminhos de pasta não abrem sozinhos no GitHub Pages)
Um site acessado pela internet em HTTPS (`https://fabbioca.github.io/`) é proibido por regras internacionais de segurança do Android e iOS de acessar silenciosamente pastas do seu disco interno apenas digitando o caminho textual (ex: `\Treinos`). Se isso fosse permitido, qualquer site malicioso poderia ler fotos ou documentos do seu aparelho.

Por isso, você tem **duas formas oficiais e práticas de usar**:

---

### Opção A: Usando pelo GitHub Pages (Online com Cache da Pasta)
1. Coloque seus vídeos na pasta `\Treinos` da memória interna do celular.
2. Abra o app pelo link: `https://fabbioca.github.io/Treinos/`.
3. Na primeira vez, toque em **Configurar Pasta > Selecionar Pasta de Vídeos** e escolha a pasta `\Treinos`.
4. **O que mudou agora:** O app salva a chave de acesso da pasta no banco de dados interno do navegador (**IndexedDB**).
5. **Ao reabrir o app nos próximos dias:** O app lembrará da pasta `Treinos` salva. Basta dar **1 toque no botão `▶ Ativar Vídeos`** (ou simplesmente tocar em qualquer aula para assistir) e o navegador reativa a reprodução instantaneamente, sem precisar navegar por pastas novamente!

---

### Opção B: Usando 100% Local (Mesma Pasta dos Vídeos — Zero Prompts)
Se você não quer precisar dar nem 1 toque para ativar a pasta dos vídeos:
1. Copie o arquivo `APP_TREINO_V11.html` para **dentro da mesma pasta `\Treinos`** onde estão os 21 vídeos no seu celular.
2. Abra o arquivo `APP_TREINO_V11.html` diretamente no seu celular (via Chrome, Samsung Internet ou gerenciador de arquivos).
3. Como o HTML está na mesma pasta dos vídeos, ele carrega os vídeos **diretamente via `./` sem nenhuma restrição de navegador e sem nunca pedir permissão**.
4. **Como atualizar o app no futuro sem conectar no PC:**
   - Sempre que você fizer alterações no código pelo computador e subir no GitHub:
   - Abra o app, toque no ícone de engrenagem ⚙️ (topo) e clique em **⬇️ Baixar APP_TREINO_V11.html do GitHub**.
   - O app baixa a nova versão atualizada em 1 segundo direto para o seu celular. Substitua o arquivo na pasta `\Treinos` e pronto!

---

## 5. Recursos e Funcionalidades do App

### 5.1. Treino V10 e Sobrecarga Progressiva (Última Carga Salva)
- **Código da Máquina:** cada exercício exibe o código RealLeader (`#01`–`#30`, conforme [equipamentos_academia.md](file:///d:/Treinos/docs/equipamentos_academia.md)) com modelo, nome e tipo de carga, para localizar o equipamento na academia. Equipamentos clássicos (polia, crossover, Crunch Machine, Captain's Chair) aparecem com código `—`.
- **Titular × Reserva:** seletor por exercício para alternar para a máquina reserva (fila no horário de pico). A escolha é salva em `v10_machine`.
- **Última Carga por Máquina:** campo `⚖️ Última Carga` + unidade (`kg`, `lbs`, `kg/lado`, `placas`) + data do registro. Cada máquina lembra a própria carga (chave `exercício:máquina` em `v10_weights`); o placeholder mostra a carga de referência quando conhecida (ex.: `#01` 160 lbs, `#02` 40 kg/lado).
- **Retrocompatibilidade:** valores antigos (texto livre por exercício) são lidos como carga da máquina titular.
- **Persistência Total:** gravado no `localStorage` no exato momento da digitação e incluído no backup JSON (`v10_weights`, `v10_machine`).


### 5.2. Gestão do Desafio 21 Dias
- **Dashboard em Tempo Real:** Mostra total de aulas concluídas (`X / 21`), porcentagem de evolução e tempo total treinado acumulado.
- **Divisão em 3 Fases:**
  - *Fase 1 (Dias 1 a 7):* Ativação Metabólica e Ignição.
  - *Fase 2 (Dias 8 a 14):* Boom Hormonal e Aceleração.
  - *Fase 3 (Dias 15 a 21):* Definição Extrema e Seca Pochete.
- **Filtros Rápidos:** Filtre por *Todas*, *Semana 1*, *Semana 2*, *Semana 3*, *Pendentes* ou *Concluídas*.
- **Anotações de Treino:** Cada dia possui um campo de anotações expansível para registrar cargas, repetições, facilidade ou sensações de fadiga.

### 5.2. Player de Vídeo In-App Prime
- **Controle de Velocidade:** Botão rápido para alternar entre `1.0x`, `1.25x`, `1.5x` e `2.0x`.
- **Navegação no Vídeo:** Botões para retroceder ou avançar 10 segundos.
- **Ação Direta de Conclusão:** O botão *Concluir Aula* dentro do player já registra o dia como finalizado com a data e hora do término e atualiza a barra de progresso.

### 5.3. Cronômetro de Descanso Flutuante (FAB)
- Botão flutuante permanente no canto inferior direito.
- Contagem regressiva visual circular com opções padrão de 45s e 60s.
- Vibração háptica de 10 segundos no celular ao zerar o tempo para avisar o início da próxima série.

### 5.4. Segurança e Backup dos Dados
- Os dados são armazenados localmente no navegador via `localStorage`.
- No ícone de engrenagem (⚙️) no cabeçalho:
  - **Exportar Backup:** Baixa um arquivo `treinos_fabbio_backup.json` com todo o histórico de treinos e anotações.
  - **Restaurar Backup:** Importa o arquivo JSON em qualquer outro dispositivo sem perda de informações.
