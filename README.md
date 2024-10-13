- 👋 Hi, I’m @Zallag
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Zallag/Zallag is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->import pygame
import random

# Inicializar Pygame
pygame.init()

# Configurações da tela
largura_tela = 800
altura_tela = 600
tela = pygame.display.set_mode((largura_tela, altura_tela))
pygame.display.set_caption('Desfile e Amigos de Yasmin')

# Cores
branco = (255, 255, 255)
preto = (0, 0, 0)

# Variáveis do jogo
pontuacao = 0
posicao_yasmin = [400, 300]
amigos = []
tempo_novo_amigo = 5000  # Novo amigo a cada 5 segundos
ultimo_amigo = pygame.time.get_ticks()
yasmin_image = pygame.image.load('yasmin.png')  # Substitua pelo caminho da imagem da Yasmin

# Loop do jogo
executando = True
while executando:
    tempo_atual = pygame.time.get_ticks()

    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            executando = False
        elif evento.type == pygame.MOUSEBUTTONDOWN:
            x, y = evento.pos
            if posicao_yasmin[0] < x < posicao_yasmin[0] + 50 and posicao_yasmin[1] < y < posicao_yasmin[1] + 100:
                pontuacao += 1
                posicao_yasmin = [random.randint(0, largura_tela-50), random.randint(0, altura_tela-50)]
    
    # Adicionar novos amigos
    if tempo_atual - ultimo_amigo > tempo_novo_amigo:
        amigos.append([random.randint(0, largura_tela-50), random.randint(0, altura_tela-50)])
        ultimo_amigo = tempo_atual
    
    tela.fill(branco)
    tela.blit(yasmin_image, posicao_yasmin)
    
    for amigo in amigos:
        pygame.draw.circle(tela, preto, amigo, 25)
    
    fonte = pygame.font.Font(None, 36)
    texto = fonte.render(f'Amigos: {pontuacao}', True, preto)
    tela.blit(texto, (10, 10))
    pygame.display.flip()

pygame.quit()

