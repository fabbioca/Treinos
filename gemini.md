# GEMINI.md — Stack, Arquitetura e Deploy

## 1. Visão Geral do Projeto
Aplicativo web móvel (PWA / Single Page Application offline-first) para gestão e acompanhamento diário de treinos de academia e protocolos de alta intensidade para o usuário Fabbio.

### Módulos Principais:
1. **Treino Semanal V10**: Rotina de segunda a domingo (Fullbody A, B, C, Cardio Zona 2, HIIT 4×4 e Recuperação).
2. **Desafio 21 Dias (Método 40+ / Seca Pochete)**: Gestão das 21 aulas em vídeo (13 a 23 minutos), marcação de conclusão com timestamp, anotações de carga e player integrado.
3. **Dieta & 40+**: Síntese prática das refeições do desafio (café, almoço, lanche, jantar), lista de substituições de alimentos e pilares do boom hormonal (GH e Testosterona).
4. **Cronômetro Flutuante de Descanso**: FAB com contador de descanso (45s, 60s, customizado), vibração háptica e frases motivacionais.
5. **Backup & Sincronização**: Exportação e importação completa do histórico em JSON.

---

## 2. Stack Tecnológica
- **Frontend Core**: HTML5 Semântico, Vanilla JavaScript (ES6+), zero dependências de build ou npm.
- **Estilização**: Vanilla CSS3 moderno com variáveis CSS (Design System próprio, Dark Navy `#0F1F45`, Vibrant Orange `#F05A28`, Emerald Green `#059669`, tipografia Sora e Nunito Sans do Google Fonts).
- **Armazenamento de Dados**:
  - `localStorage`:
    - `v10_done`: Exercícios semanais concluídos.
    - `v10_d21_state`: Status de conclusão, datas e anotações dos 21 dias.
    - `v10_d21_config`: Caminho relativo base dos vídeos (`../videos/` ou configurável).
    - `v10_active_module`: Última aba selecionada.
  - **Mapeamento de Vídeos Locais**:
    - HTML5 Video API + File System Access API (`showDirectoryPicker`) + `<input type="file">` com `URL.createObjectURL` para execução offline sem restrição de sandbox móvel.
- **PWA**: Compatível com instalação direta na tela inicial de smartphones Android e iPhones iOS.

---

## 3. Gestão de Mídia e Repositório Git
- **Arquivos Pesados**: A pasta `videos/` contém 21 arquivos `.mp4` totalizando ~4,1 GB (com vídeos de até 367 MB).
- **Proteção do Git**: A pasta `/videos/` e extensões `*.mp4` estão registradas no `.gitignore` para respeitar o limite de 100 MB do GitHub.
- **Execução no Celular**: Os vídeos são copiados diretamente para o armazenamento do celular (ou mantidos em pasta sincronizada) e vinculados com 1 toque no app através do modal "Configurar Pasta".

---

## 4. Deploy Contínuo (CI/CD Automático via GitHub Pages)
1. **Repositório**: GitHub (`main` branch).
2. **Ponto de Entrada**: [index.html](file:///d:/Treinos/index.html) na raiz realiza redirecionamento limpo para [app/APP_TREINO_V11.html](file:///d:/Treinos/app/APP_TREINO_V11.html).
3. **Configuração do GitHub Pages**:
   - `Settings` > `Pages`
   - Source: `Deploy from a branch`
   - Branch: `main` / Folder: `/(root)`
   - Sempre que houver `git commit` e `git push`, o app é publicado e atualizado automaticamente na URL HTTPS do usuário.
