<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog Minimalista</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Special+Elite&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Special Elite', monospace;
            background-color: #ffffff;
            color: #000000;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        .suggestion-box textarea, .suggestion-box button,
        .admin-section input, .admin-section textarea, .admin-section button { /* Aplicar fonte aos elementos do admin */
            font-family: 'Special Elite', monospace;
        }

        .content-section h2, .content-section h3 {
            margin-top: 1.5em;
            margin-bottom: 0.5em;
        }
        .content-section p {
            line-height: 1.7;
            margin-bottom: 1.2em;
        }
        .content-section blockquote {
            border-left: 2px solid #000;
            padding-left: 1em;
            margin-left: 0;
            margin-top: 1.5em;
            margin-bottom: 1.5em;
            font-style: normal;
        }
        .content-section a {
            text-decoration: underline;
            color: #000000;
        }
        .content-section a:hover {
            background-color: #f0f0f0;
        }

        .suggestion-box textarea::placeholder,
        .admin-section input::placeholder, .admin-section textarea::placeholder { /* Estilo placeholder admin */
            color: #555555;
        }

        /* Classes utilitárias para mostrar/esconder seções */
        .hidden {
            display: none;
        }

        /* Estilo para botões de ação no admin */
        .admin-action-btn {
            @apply px-3 py-1.5 text-xs border border-black rounded-md hover:bg-gray-200 transition-colors duration-150;
        }
        .admin-delete-btn {
            @apply px-3 py-1.5 text-xs border border-red-700 text-red-700 rounded-md hover:bg-red-100 transition-colors duration-150;
        }

    </style>
</head>
<body class="min-h-screen container mx-auto p-4 sm:p-6 md:p-8 selection:bg-gray-300 selection:text-black">

    <div id="publicView">
        <header class="text-center py-8 sm:py-12">
            <h1 class="text-4xl sm:text-5xl font-bold">CRÔNICAS DA MÁQUINA</h1>
            <p class="text-sm sm:text-base mt-2">Pensamentos em Preto & Branco.</p>
        </header>

        <main class="max-w-2xl mx-auto">
            <article id="mainArticle" class="mb-12 sm:mb-16 content-section">
                <p class="text-center py-10">Carregando post...</p>
            </article>

            <section class="suggestion-box py-8 sm:py-10 border-t-2 border-black">
                <h3 class="text-xl sm:text-2xl font-semibold mb-4">Deixe sua Contribuição</h3>
                <p class="mb-4 text-sm">Encontrou algo que poderia ser aprimorado, uma ideia a acrescentar, ou um simples erro de digitação? Por favor, compartilhe abaixo. Para facilitar, copie e cole o trecho original do texto e, em seguida, sua sugestão.</p>
                <form id="suggestionForm" class="space-y-4">
                    <div>
                        <label for="suggestionText" class="block text-sm font-medium mb-1 sr-only">Sua Sugestão:</label>
                        <textarea id="suggestionText" name="suggestionText" rows="7" class="w-full p-3 border-2 border-black rounded-md focus:ring-1 focus:ring-black focus:border-black bg-white text-black placeholder-gray-600" placeholder="Ex: No parágrafo 'A escolha por uma estética minimalista...', sugiro alterar 'contemplação' para 'reflexão profunda'."></textarea>
                    </div>
                    <div class="text-right">
                        <button type="submit" class="px-8 py-3 bg-black text-white rounded-md hover:bg-gray-800 active:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-black focus:ring-opacity-50 transition-colors duration-150">Enviar Sugestão</button>
                    </div>
                </form>
                <div id="feedbackMessage" class="mt-4 text-sm" role="alert"></div>
            </section>
        </main>

        <footer class="text-center py-8 sm:py-10 mt-12 sm:mt-16 border-t-2 border-black">
            <p class="text-xs">&copy; <span id="currentYearPublic"></span> Crônicas da Máquina. Minimalismo em progresso.</p>
        </footer>
    </div>

    <div id="adminView" class="hidden admin-section">
        <header class="text-center py-8 sm:py-12">
            <h1 class="text-3xl sm:text-4xl font-bold">Área de Administração</h1>
            <p class="text-sm sm:text-base mt-2">Gerenciamento de Conteúdo</p>
        </header>

        <main class="max-w-3xl mx-auto">
            <section id="postFormContainer" class="mb-10 p-6 border-2 border-black rounded-md">
                <h2 id="formTitle" class="text-2xl font-semibold mb-4">Adicionar Novo Post</h2>
                <form id="postForm" class="space-y-4">
                    <input type="hidden" id="postId" name="postId">
                    <div>
                        <label for="postTitle" class="block text-sm font-medium mb-1">Título:</label>
                        <input type="text" id="postTitle" name="postTitle" required class="w-full p-2 border-2 border-black rounded-md bg-white text-black placeholder-gray-600">
                    </div>
                    <div>
                        <label for="postContent" class="block text-sm font-medium mb-1">Conteúdo (HTML permitido para parágrafos, blockquotes, etc.):</label>
                        <textarea id="postContent" name="postContent" rows="10" required class="w-full p-2 border-2 border-black rounded-md bg-white text-black placeholder-gray-600"></textarea>
                    </div>
                    <div class="flex justify-end space-x-3">
                        <button type="button" id="cancelEditBtn" class="px-6 py-2 border-2 border-black rounded-md hover:bg-gray-200 hidden">Cancelar</button>
                        <button type="submit" id="savePostBtn" class="px-8 py-2 bg-black text-white rounded-md hover:bg-gray-800">Salvar Post</button>
                    </div>
                </form>
            </section>

            <section>
                <h2 class="text-2xl font-semibold mb-4">Posts Existentes</h2>
                <div id="adminPostList" class="space-y-4">
                    <p>Nenhum post encontrado.</p>
                </div>
            </section>
        </main>

        <footer class="text-center py-8 sm:py-10 mt-12 sm:mt-16 border-t-2 border-black">
             <p class="text-xs">&copy; <span id="currentYearAdmin"></span> Modo Administrador.</p>
        </footer>
    </div>

    <div class="text-center py-6 border-t-2 border-black mt-8">
        <button id="toggleViewBtn" class="underline hover:text-gray-700">Acessar Área de Administração</button>
    </div>

    <script>
        // --- DADOS SIMULADOS (Posts do Blog) ---
        let posts = [
            {
                id: '1',
                title: 'Reflexões Sob a Luz Pálida da Tela',
                // Conteúdo em HTML para ser renderizado corretamente
                content: `
                    <p class="text-xs text-gray-700 mb-6">Publicado em <span class="post-date-dynamic"></span></p>
                    <p>No silêncio do quarto, apenas o teclar rítmico quebra a quietude. Cada letra surge na tela como um pequeno fantasma, uma ideia materializada em pixels pretos sobre um fundo branco imaculado. Este é o ofício: traduzir o caos interno em linhas ordenadas, buscar sentido onde talvez não haja nenhum.</p>
                    <p>A escolha por uma estética minimalista não é acidental. É um reflexo da busca pela essência, pelo despojamento do supérfluo. Em um mundo saturado de cores vibrantes e estímulos constantes, o preto e branco oferece um refúgio, um espaço para a contemplação. A fonte, reminiscente das antigas máquinas de escrever, evoca uma nostalgia por um tempo onde as palavras pareciam ter mais peso, cada caractere impresso com esforço e permanência.</p>
                    <blockquote><p>"Escrever é fácil. Você apenas encara uma folha de papel em branco até que gotas de sangue comecem a se formar na sua testa." - Gene Fowler (atribuído)</p></blockquote>
                    <p>Este espaço é um convite ao diálogo. As palavras aqui dispostas são apenas um ponto de partida. Se alguma frase ressoar, se uma ideia provocar um pensamento divergente, ou se você simplesmente notar um erro de digitação que escapou aos meus olhos cansados, sua contribuição é bem-vinda. Utilize a caixa de sugestões ao final da página. Aponte o trecho, compartilhe sua perspectiva.</p>
                    <h3 class="text-xl sm:text-2xl font-semibold mt-8 mb-3">A Arte da Imperfeição</h3>
                    <p>Não busco a perfeição, pois ela é uma miragem. Busco a honestidade, a expressão crua. Cada texto é um instantâneo, um fragmento de um pensamento em evolução. As sugestões dos leitores podem polir as arestas, adicionar novas camadas de significado, ou simplesmente corrigir um deslize. E tudo isso faz parte do processo.</p>
                    <p>Obrigado por dedicar seu tempo a estas linhas.</p>
                `,
                publishedDate: new Date().toISOString() // Data de publicação inicial
            }
        ];

        // --- ELEMENTOS DO DOM ---
        const publicView = document.getElementById('publicView');
        const adminView = document.getElementById('adminView');
        const toggleViewBtn = document.getElementById('toggleViewBtn');
        
        // Elementos da Visualização Pública
        const mainArticle = document.getElementById('mainArticle');
        const suggestionForm = document.getElementById('suggestionForm');
        const feedbackMessage = document.getElementById('feedbackMessage');
        const suggestionTextarea = document.getElementById('suggestionText');

        // Elementos da Área de Admin
        const postFormContainer = document.getElementById('postFormContainer');
        const postForm = document.getElementById('postForm');
        const formTitle = document.getElementById('formTitle');
        const postIdInput = document.getElementById('postId');
        const postTitleInput = document.getElementById('postTitle');
        const postContentInput = document.getElementById('postContent');
        const cancelEditBtn = document.getElementById('cancelEditBtn');
        const savePostBtn = document.getElementById('savePostBtn');
        const adminPostList = document.getElementById('adminPostList');

        // --- FUNÇÕES ---

        // Função para formatar data
        function formatDate(dateString) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            return new Date(dateString).toLocaleDateString('pt-BR', options);
        }
        
        // Renderizar o post principal na visualização pública
        function renderPublicPost() {
            if (posts.length > 0) {
                // Por simplicidade, sempre mostra o primeiro post.
                // Em um blog real, haveria navegação entre posts.
                const postToDisplay = posts[0]; 
                mainArticle.innerHTML = `
                    <h2 class="text-2xl sm:text-3xl font-semibold mb-4">${postToDisplay.title}</h2>
                    ${postToDisplay.content}
                `;
                // Atualizar data dinâmica dentro do conteúdo do post
                const dateElement = mainArticle.querySelector('.post-date-dynamic');
                if(dateElement) {
                    dateElement.textContent = formatDate(postToDisplay.publishedDate);
                }
            } else {
                mainArticle.innerHTML = '<p class="text-center py-10">Nenhum post para exibir.</p>';
            }
        }

        // Renderizar lista de posts na área de admin
        function renderAdminPosts() {
            adminPostList.innerHTML = ''; // Limpa a lista atual
            if (posts.length === 0) {
                adminPostList.innerHTML = '<p>Nenhum post encontrado. Adicione um novo!</p>';
                return;
            }
            posts.forEach(post => {
                const postElement = document.createElement('div');
                postElement.className = 'p-4 border-2 border-gray-300 rounded-md flex justify-between items-center';
                postElement.innerHTML = `
                    <div>
                        <h4 class="text-lg font-semibold">${post.title}</h4>
                        <p class="text-xs text-gray-600">Publicado em: ${formatDate(post.publishedDate)}</p>
                    </div>
                    <div class="space-x-2">
                        <button class="admin-action-btn edit-btn" data-id="${post.id}">Editar</button>
                        <button class="admin-delete-btn delete-btn" data-id="${post.id}">Excluir</button>
                    </div>
                `;
                adminPostList.appendChild(postElement);
            });

            // Adicionar event listeners para os novos botões de editar/excluir
            document.querySelectorAll('.edit-btn').forEach(button => {
                button.addEventListener('click', handleEditPost);
            });
            document.querySelectorAll('.delete-btn').forEach(button => {
                button.addEventListener('click', handleDeletePost);
            });
        }

        // Mostrar formulário de edição/adição
        function showPostForm(post = null) {
            if (post) { // Editando
                formTitle.textContent = 'Editar Post';
                postIdInput.value = post.id;
                postTitleInput.value = post.title;
                postContentInput.value = post.content.replace(/<p class="text-xs text-gray-700 mb-6">Publicado em <span class="post-date-dynamic">.*?<\/span><\/p>\s*/, '').trim(); // Remove a data do conteúdo para edição
                savePostBtn.textContent = 'Salvar Alterações';
                cancelEditBtn.classList.remove('hidden');
            } else { // Adicionando
                formTitle.textContent = 'Adicionar Novo Post';
                postForm.reset(); // Limpa o formulário
                postIdInput.value = '';
                savePostBtn.textContent = 'Salvar Post';
                cancelEditBtn.classList.add('hidden');
            }
            // postFormContainer.classList.remove('hidden'); // O formulário está sempre visível
        }

        // Cancelar edição
        cancelEditBtn.addEventListener('click', () => {
            showPostForm(); // Reseta para o modo "Adicionar Novo Post"
        });
        
        // Manipular submissão do formulário de post (Adicionar/Editar)
        postForm.addEventListener('submit', function(event) {
            event.preventDefault();
            const id = postIdInput.value;
            const title = postTitleInput.value.trim();
            const content = postContentInput.value.trim(); // Conteúdo HTML bruto
            
            if (!title || !content) {
                alert('Título e conteúdo são obrigatórios.'); // Usando alert temporariamente para feedback simples
                return;
            }

            // Adicionar a data de publicação ao conteúdo se for um novo post ou se não existir
            const dateHtml = `<p class="text-xs text-gray-700 mb-6">Publicado em <span class="post-date-dynamic">${formatDate(new Date().toISOString())}</span></p>\n`;
            const finalContent = dateHtml + content;

            if (id) { // Editando post existente
                const postIndex = posts.findIndex(p => p.id === id);
                if (postIndex > -1) {
                    posts[postIndex].title = title;
                    posts[postIndex].content = finalContent; 
                    // Manter a data de publicação original se já existir, ou atualizar se necessário
                    posts[postIndex].publishedDate = posts[postIndex].publishedDate || new Date().toISOString();
                }
            } else { // Adicionando novo post
                const newPost = {
                    id: Date.now().toString(), // ID simples baseado no timestamp
                    title: title,
                    content: finalContent,
                    publishedDate: new Date().toISOString()
                };
                posts.unshift(newPost); // Adiciona no início para ser o post mais recente
            }
            
            renderAdminPosts();
            renderPublicPost(); // Atualiza a visualização pública também
            showPostForm(); // Reseta o formulário para "Adicionar Novo"
            // postFormContainer.classList.add('hidden'); // O formulário está sempre visível
        });

        // Manipular clique no botão Editar
        function handleEditPost(event) {
            const postId = event.target.dataset.id;
            const postToEdit = posts.find(p => p.id === postId);
            if (postToEdit) {
                showPostForm(postToEdit);
                window.scrollTo({ top: postFormContainer.offsetTop - 20, behavior: 'smooth' }); // Rola para o formulário
            }
        }

        // Manipular clique no botão Excluir
        function handleDeletePost(event) {
            const postId = event.target.dataset.id;
            // Adicionar uma confirmação básica (em um app real, usar um modal customizado)
            // Como não podemos usar confirm(), vamos deletar diretamente para este exemplo.
            // console.warn("Em um app real, adicione uma confirmação customizada aqui antes de deletar.");
            
            posts = posts.filter(p => p.id !== postId);
            renderAdminPosts();
            renderPublicPost(); // Atualiza a visualização pública
            
            // Se o post excluído era o que estava sendo editado, reseta o formulário
            if(postIdInput.value === postId) {
                showPostForm();
            }
        }

        // Alternar entre visualização pública e admin
        toggleViewBtn.addEventListener('click', function() {
            if (publicView.classList.contains('hidden')) {
                // Mudar para Visualização Pública
                publicView.classList.remove('hidden');
                adminView.classList.add('hidden');
                toggleViewBtn.textContent = 'Acessar Área de Administração';
                renderPublicPost(); // Garante que o post público está atualizado
            } else {
                // Mudar para Área de Admin
                publicView.classList.add('hidden');
                adminView.classList.remove('hidden');
                toggleViewBtn.textContent = 'Ver Site Público';
                renderAdminPosts(); // Garante que a lista de posts no admin está atualizada
                showPostForm(); // Garante que o formulário de post está no estado inicial
            }
        });

        // Manipulação do formulário de sugestão (da visualização pública)
        if (suggestionForm) {
            suggestionForm.addEventListener('submit', function(event) {
                event.preventDefault();
                const suggestion = suggestionTextarea.value.trim();

                if (suggestion === "") {
                    feedbackMessage.textContent = "Por favor, escreva uma sugestão antes de enviar.";
                    feedbackMessage.className = "mt-4 text-sm text-red-700 font-semibold";
                    suggestionTextarea.focus();
                    return;
                }
                console.log("Sugestão Recebida (simulação):", suggestion);
                feedbackMessage.textContent = "Obrigado pela sua sugestão! Ela foi 'enviada' para revisão.";
                feedbackMessage.className = "mt-4 text-sm text-green-700 font-semibold";
                suggestionTextarea.value = '';
                setTimeout(() => {
                    feedbackMessage.textContent = "";
                    feedbackMessage.className = "mt-4 text-sm"; 
                }, 7000);
            });
        }
        
        // --- INICIALIZAÇÃO ---
        function initializeApp() {
            document.getElementById('currentYearPublic').textContent = new Date().getFullYear();
            document.getElementById('currentYearAdmin').textContent = new Date().getFullYear();
            renderPublicPost(); // Carrega o post inicial na visualização pública
            // A área de admin é renderizada quando ativada
        }

        initializeApp();

    </script>

</body>
</html>
