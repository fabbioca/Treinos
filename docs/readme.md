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

## 4. Guia de Cópia e Vinculação dos Vídeos no Celular

Para ter os 21 vídeos disponíveis na academia sem depender de sinal de internet ou gastar dados 4G:

### 4.1. Como copiar os vídeos para o celular:
1. Conecte seu celular ao computador via cabo USB (ou envie via pendrive OTG / AirDrop / compartilhamento de rede).
2. Crie uma pasta chamada `videos` no seu celular (por exemplo, na pasta `Downloads/videos` ou `Documentos/videos`).
3. Copie os 21 arquivos `Desafio DIA 01.mp4` até `Desafio DIA 21.mp4` para essa pasta no celular.

### 4.2. Como vincular no aplicativo:
1. Abra o app no seu navegador do celular (ou instale o ícone na tela inicial).
2. Na aba **🔥 Desafio 21 Dias**, clique no botão **Configurar Pasta** no topo.
3. Escolha uma das opções:
   - **Opção 1 (Selecionar Pasta):** Toque em *Selecionar Pasta de Vídeos* e aponte para a pasta `videos` criada. O app vinculará todas as 21 aulas de uma só vez.
   - **Opção 2 (Selecionar Múltiplos Arquivos):** Caso seu navegador no celular restrinja a seleção de pasta inteira, toque em *Selecionar os 21 Arquivos MP4*, selecione todos os vídeos e confirme.
   - **Opção 3 (Arquivo Individual):** Se preferir, ao clicar em *Assistir Aula* em qualquer dia, caso o vídeo não seja encontrado de imediato, o próprio player exibirá o botão *Escolher Arquivo do Vídeo* para você tocar no arquivo daquele dia específico.

---

## 5. Recursos e Funcionalidades do App

### 5.1. Gestão do Desafio 21 Dias
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
