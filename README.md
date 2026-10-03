🔬 Explorador 3D de Expressão Gênica: PCA, Efeito de Batch e k-means

Ferramenta educacional, 100% no navegador, para visualizar em 3D como o efeito de batch (variação técnica entre lotes de experimento) pode distorcer a análise de dados de expressão gênica, e como a correção muda o resultado.

⚠️ Projeto educacional. Os dados padrão são sintéticos e a correção de batch é uma versão simplificada. Não é uma ferramenta para análise clínica ou publicação científica.

🎯 O problema

Em experimentos de RNA-seq e single-cell, amostras processadas em dias, equipamentos ou laboratórios diferentes carregam diferenças técnicas, os batch effects. Se não forem tratados, algoritmos de agrupamento podem separar as amostras por lote em vez de por biologia, levando a "descobertas" que são só artefatos.

Este projeto permite ver isso acontecer e comparar antes e depois da correção.

✨ Funcionalidades
Arquivo	O que faz
explorador-3d-v2.html	Versão completa: PCA 3D interativo, upload de CSV, correção de batch, transformação log2(x+1), k-means e métricas de pureza
explorador-3d-batch.html	Primeira versão: PCA 3D com dados sintéticos e controle de batch/ruído
simulador-mutacoes.html	Simulador de mutações pontuais: DNA → códons → proteína (silenciosa, missense, nonsense)

Na v2:

Gráfico 3D rotacionável (arraste com mouse ou dedo)
Sliders para intensidade do efeito de batch e ruído técnico (dados sintéticos)
Correção de batch por centralização de cada gene dentro de cada lote
Cor por grupo, batch ou cluster encontrado
Pureza do agrupamento: mostra quanto os clusters do k-means coincidem com o grupo biológico e quanto coincidem com o batch
Carregamento de CSV próprio e download de CSV de exemplo
🚀 Como usar

Não precisa instalar nada.

Baixe os arquivos .html
Dê dois cliques para abrir no navegador (ou publique via GitHub Pages)

Experimento sugerido:

Abra a v2 com efeito de batch em ~3 e observe a pureza por batch e por grupo
Marque "Corrigir batch"
Compare: a pureza biológica deve subir e a pureza por batch deve cair
📄 Formato do CSV
csv
id,grupo,lote,gene1,gene2,gene3
c1,Tipo A,Lote 1,5.21,3.10,0.88
c2,Tipo B,Lote 2,1.02,4.55,2.31
1ª coluna: id da amostra · 2ª: grupo (ex.: tipo celular) · 3ª: lote (batch) · demais: genes (números)
Separador: vírgula, ponto e vírgula ou tab
Limite: as primeiras 800 amostras são lidas
⚙️ Como funciona
Dados: sintéticos (3 tipos celulares × 2 lotes) ou CSV carregado
Pré-processamento (opcional): log2(x+1) e correção de batch (subtrai a média do gene no lote e soma a média global)
PCA implementado do zero em JavaScript: matriz de similaridade entre amostras e iteração de potência para os 3 primeiros componentes
k-means no espaço dos 3 PCs, com k igual ao número de grupos e inicialização por ponto mais distante
Pureza: fração de amostras que pertence ao rótulo majoritário de seu cluster
Visualização: projeção 3D com perspectiva desenhada em <canvas>, sem bibliotecas externas
🚧 Limitações
Correção de batch simples (centralização), bem mais básica que ComBat, Harmony ou Seurat
PCA e k-means calculados no navegador, adequados para até ~800 amostras
k-means pode variar com dados reais e depende da escolha de k
A pureza é calculada no espaço 3D dos PCs, e não nos dados originais
Dados sintéticos não reproduzem toda a complexidade de dados biológicos reais
🗺️ Próximos passos
 Testar com dataset público real (ex.: NCBI GEO)
 Adicionar UMAP / t-SNE
 Reescrever a análise em Python (scikit-learn / scanpy) e usar o front-end só para visualização
 Comparar com ComBat/Harmony
🤖 Transparência

Este projeto foi desenvolvido com auxílio de IA (Claude, da Anthropic) e adaptado/estudado por mim como parte do meu aprendizado em bioinformática.

👩‍💻 Autora

Taciane · Biomedicina + Programação
LinkedIn · GitHub

 Fique à vontade para estudar, modificar e compartilhar.
