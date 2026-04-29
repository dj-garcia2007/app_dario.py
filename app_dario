import streamlit as st 
import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt


####################
## ajustar el layout
#################### 

st.set_page_config(layout="wide")


##################
## tamaño del plot
################## 

fig, ax = plt.subplots()


#########
## titulo
######### 

col1,col2,col3 = st.columns([1,2,1])

col1.image("logouprh.png", width=150)
col2.title("Datos de Covid - Variante Omicrón")
col3.image("covid.png", width=150)

##############################################
## esto es para que salga una linea horizontal
############################################## 

st.divider()

#################
## datos de covid 
################# 

df_covid = pd.read_csv("https://raw.githubusercontent.com/elioramosweb/archivo_datos/main/datos_diarios-2022-03-22_10_20_15.csv",parse_dates=['date'])

df_covid["date"] = pd.to_datetime(df_covid["date"])

## selecionar columnas
nombres = list(df_covid.columns)[1:]

columna = st.sidebar.selectbox("Columna de interes", nombres)

df_covid.plot(x="date", y=columna, ax=ax,ylabel=columna,linewidth=3,linestyle="dotted")

col1,col2 = st.columns(2)

st.sidebar.divider()

suavizado = st.sidebar.checkbox("Suavizado")

if suavizado:
    ventana = st.sidebar.slider("Ventana de suavizado [días]", 1, 15, 7)
    df_rolling = df_covid[columna].rolling(window=ventana,center=True).mean()
    df_covid[columna + "_rolling"] = df_rolling
    df_covid.plot(x="date", y=columna + "_rolling", ax=ax)

st.sidebar.divider()

tabla = st.sidebar.checkbox("Mostrar datos")

if tabla:
    df_covid["date"] = df_covid["date"].dt.strftime("%d-%b-%Y")
    df_tabla = df_covid[["date",columna]]
    col2.write(df_tabla)

st.sidebar.markdown(""" Aplicación desarrollada por: 
                    Darío J. 
                    Comp3082""")
col1.pyplot(fig)
