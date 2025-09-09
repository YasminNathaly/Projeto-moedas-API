#Projeto de consumir api
# 📊 Cotação de Moedas - Streamlit + AwesomeAPI

Projeto simples em **Python** que usa [Streamlit](https://streamlit.io/) e a [AwesomeAPI](https://docs.awesomeapi.com.br/api-de-moedas) para buscar a cotação de moedas em tempo real.

---

## 🔧 Pré-requisitos

- [Python 3.9+](https://www.python.org/downloads/)
- Pip (gerenciador de pacotes do Python)

Verifique se já possui Python e pip instalados:
```bash
python --version
pip --version

import streamlit as st
import requests

st.title("Cotação de Moedas - AwesomeAPI")

moedas = {
    "Dólar → Real": "USD-BRL",
    "Euro → Real": "EUR-BRL",
    "Bitcoin → Real": "BTC-BRL",
    "Libra → Real": "GBP-BRL"
}

opcao = st.selectbox("Selecione a cotação:", list(moedas.keys()))

if st.button("Buscar cotação"):
    url = f"https://economia.awesomeapi.com.br/json/last/{moedas[opcao]}"
    resposta = requests.get(url)

    if resposta.status_code == 200:
        dados = resposta.json()
        chave = list(dados.keys())[0]  # exemplo: "USDBRL"
        info = dados[chave]

        st.subheader(info["name"])
        st.write(f"**Alta do dia:** {info['high']}")
        st.write(f"**Baixa do dia:** {info['low']}")
        st.write(f"**Variação:** {info['varBid']}")
        st.write(f"**Cotação atual (compra):** R$ {info['bid']}")
        st.write(f"**Cotação atual (venda):** R$ {info['ask']}")
    else:
        st.error("Erro ao buscar a cotação.")
