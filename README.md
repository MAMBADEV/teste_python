import streamlit as st
import datetime

# Configuração da página
st.set_page_config(
    page_title="Visionários do Amanhã: Afrofuturismo",
    page_icon="✨",
    layout="centered"
)

# --- ESTILIZAÇÃO CUSTOMIZADA (CSS) ---
st.markdown(f"""
    <style>
    @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Montserrat:wght@300;400&display=swap');

    .main {{
        background-color: #000000;
        color: #C0C0C0; /* Prata */
        font-family: 'Montserrat', sans-serif;
    }}
    
    h1, h2, h3 {{
        font-family: 'Playfair Display', serif;
        color: #D4AF37; /* Ouro */
        text-align: center;
    }}

    .stButton>button {{
        background-color: #4B3621; /* Marrom */
        color: #D4AF37;
        border: 2px solid #D4AF37;
        border-radius: 20px;
        transition: 0.3s;
        width: 100%;
        font-weight: bold;
    }}

    .stButton>button:hover {{
        background-color: #D4AF37;
        color: #000000;
        border: 2px solid #C0C0C0;
    }}

    .vision-card {{
        background-color: #1a1a1a;
        padding: 20px;
        border-radius: 15px;
        border-left: 5px solid #D4AF37;
        margin-bottom: 20px;
        box-shadow: 5px 5px 15px rgba(0,0,0,0.5);
    }}

    .vision-author {{
        color: #8B4513; /* Marrom mais claro */
        font-size: 0.8rem;
        text-transform: uppercase;
        letter-spacing: 2px;
    }}

    .vision-content {{
        color: #E0E0E0;
        font-size: 1.1rem;
        font-style: italic;
    }}

    /* Estilo do Input */
    .stTextInput>div>div>input, .stTextArea>div>div>textarea {{
        background-color: #0a0a0a;
        color: #D4AF37;
        border: 1px solid #4B3621;
    }}
    </style>
    """, unsafe_allow_html=True)

# --- LÓGICA DE ARMAZENAMENTO ---
# (Em uma app real, usaríamos um banco de dados. Aqui usaremos session_state)
if 'visoes' not in st.session_state:
    st.session_state.visoes = [
        {"autor": "Anciã do Futuro", "texto": "Cidades flutuantes movidas por energia solar e o som dos tambores ecoando no silêncio do espaço.", "data": "2024"},
        {"autor": "Nzinga Tech", "texto": "Sistemas de irrigação nanotecnológicos baseados em padrões de tecelagem Kente.", "data": "2024"}
    ]

# --- INTERFACE ---

# Cabeçalho
st.markdown("<h1>SANKOFA: VISÕES AFROFUTURISTAS</h1>", unsafe_allow_html=True)
st.markdown("<p style='text-align: center; color: #C0C0C0;'>Escreva o futuro que seus ancestrais sonharam. Elegante, tecnológico e enraizado.</p>", unsafe_allow_html=True)
st.markdown("---")

# Formulário de Entrada
with st.container():
    st.markdown("### 🖋️ Registre sua Profecia")
    col1, col2 = st.columns([2, 1])
    
    with col1:
        nova_visao = st.text_area("Descreva um futuro possível e bonito:", placeholder="Ex: Robótica orgânica integrada à flora africana...")
    with col2:
        autor = st.text_input("Seu nome ou linhagem:", placeholder="Ex: Jovem Visionário")
        
    if st.button("MANIFESTAR"):
        if nova_visao and autor:
            nova_entrada = {
                "autor": autor,
                "texto": nova_visao,
                "data": datetime.datetime.now().strftime("%Y")
            }
            st.session_state.visoes.insert(0, nova_entrada)
            st.success("Visão registrada na teia do tempo!")
        else:
            st.warning("Por favor, preencha sua visão e seu nome.")

st.markdown("### 🏺 Galeria de Futuros")

# Exibição das Visões
for v in st.session_state.visoes:
    st.markdown(f"""
        <div class="vision-card">
            <div class="vision-author">{v['autor']} • {v['data']}</div>
            <div class="vision-content">"{v['texto']}"</div>
        </div>
    """, unsafe_allow_html=True)

# Rodapé
st.markdown("---")
st.markdown("<p style='text-align: center; color: #4B3621; font-size: 0.7rem;'>O futuro é um retorno às nossas origens. ✨</p>", unsafe_allow_html=True)
