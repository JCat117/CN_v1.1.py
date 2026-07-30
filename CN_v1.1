import streamlit as st
import pandas as pd
from datetime import date
import os
import json
import uuid

# ----------------------------------------------------------------------------
# CONFIGURACIÓN DE PÁGINA
# ----------------------------------------------------------------------------
st.set_page_config(
    page_title="Sistema de Control de Cianuración",
    page_icon="⚗️",
    layout="centered",
)

COLUMNS = [
    "Fecha", "Tanque", "Volumen", "Ley Cabeza",
    "Ley Cola", "Cianuro", "Cal (fundas)", "Oro Recuperado (g)"
]

TANQUE_OPTIONS = [
    "A1", "A2", "A3", "A4", "A5", "A6", "A7", "A8", "A9", "A10", "A11", "A12",
    "B1", "B2", "B3", "B4", "B5", "B6", "B7",
    "C1", "C2", "C3", "C4", "C5", "C6",
]
VOLUMEN_OPTIONS = [3, 4, 5, 6, 7, 18, 20, 25]
CIANURO_OPTIONS = [10, 20, 30, 40, 50]
CAL_OPTIONS = [0.25, 0.50, 0.75, 1.00]

ESTRUCTURA_FILE = "estructura.json"

# ----------------------------------------------------------------------------
# ESTRUCTURA: MINERAS -> PROCESOS
# Se guarda en un JSON con IDs fijos, así renombrar no afecta los archivos
# de datos ya guardados.
# ----------------------------------------------------------------------------
def cargar_estructura() -> dict:
    if os.path.exists(ESTRUCTURA_FILE):
        with open(ESTRUCTURA_FILE, "r", encoding="utf-8") as f:
            return json.load(f)
    return {}

def guardar_estructura(estructura: dict):
    with open(ESTRUCTURA_FILE, "w", encoding="utf-8") as f:
        json.dump(estructura, f, ensure_ascii=False, indent=2)

def nuevo_id() -> str:
    return str(uuid.uuid4())[:8]

# ----------------------------------------------------------------------------
# CARGA / GUARDADO DE DATOS (un CSV por combinación minera + proceso)
# ----------------------------------------------------------------------------
def archivo_registros(minera_id: str, proceso_id: str) -> str:
    return f"registros_{minera_id}_{proceso_id}.csv"

def cargar_datos(minera_id: str, proceso_id: str) -> pd.DataFrame:
    ruta = archivo_registros(minera_id, proceso_id)
    if os.path.exists(ruta):
        df = pd.read_csv(ruta, parse_dates=["Fecha"])
        if "Cal" in df.columns and "Cal (fundas)" not in df.columns:
            df = df.rename(columns={"Cal": "Cal (fundas)"})
        for col in COLUMNS:
            if col not in df.columns:
                df[col] = 0
        return df[COLUMNS].reset_index(drop=True)
    return pd.DataFrame(columns=COLUMNS)

def guardar_datos(df: pd.DataFrame, minera_id: str, proceso_id: str):
    df.to_csv(archivo_registros(minera_id, proceso_id), index=False)

# ----------------------------------------------------------------------------
# ESTILOS
# ----------------------------------------------------------------------------
st.markdown("""
<style>
    .main { font-family: 'Courier New', monospace; }
    h1, h2, h3 { font-family: 'Courier New', monospace; }
    div[data-testid="stMetric"] {
        background-color: #f0f2f6;
        padding: 15px;
        border-radius: 8px;
    }
</style>
""", unsafe_allow_html=True)

# ----------------------------------------------------------------------------
# ENCABEZADO
# ----------------------------------------------------------------------------
st.title("⚗️ SISTEMA DE CONTROL DE CIANURACIÓN")

estructura = cargar_estructura()

# ============================================================================
# NIVEL 1: MINERA
# ============================================================================
st.subheader("🏭 Minera")

nombres_minas = {mid: info["nombre"] for mid, info in estructura.items()}

col1, col2 = st.columns([2, 1])

with col1:
    if nombres_minas:
        ids_minas = list(nombres_minas.keys())
        nombres_lista = list(nombres_minas.values())
        idx_default = 0
        if st.session_state.get("minera_id") in ids_minas:
            idx_default = ids_minas.index(st.session_state["minera_id"])
        nombre_minera_sel = st.selectbox(
            "Base de datos activa", options=nombres_lista, index=idx_default, key="select_minera"
        )
        minera_id_sel = ids_minas[nombres_lista.index(nombre_minera_sel)]
    else:
        minera_id_sel = None
        st.info("Aún no has creado ninguna minera. Escribe un nombre y presiona 'Agregar' →")

with col2:
    st.write("")
    st.write("")
    nueva_minera = st.text_input(
        "Agregar nueva minera", placeholder="Ej: La Pangui S.A", key="nueva_minera_input"
    )
    if st.button("➕ Agregar minera", use_container_width=True):
        nombre = nueva_minera.strip()
        if not nombre:
            st.warning("Escribe un nombre para la minera.")
        else:
            mid = nuevo_id()
            estructura[mid] = {"nombre": nombre, "procesos": {}}
            guardar_estructura(estructura)
            st.session_state.minera_id = mid
            st.session_state.pop("proceso_id", None)
            st.rerun()

if minera_id_sel is not None:
    st.session_state.minera_id = minera_id_sel

    with st.expander("✏️ Renombrar minera seleccionada"):
        nuevo_nombre_minera = st.text_input(
            "Nuevo nombre", value=estructura[minera_id_sel]["nombre"], key="rename_minera_input"
        )
        if st.button("Guardar nuevo nombre", key="rename_minera_btn"):
            limpio = nuevo_nombre_minera.strip()
            if limpio:
                estructura[minera_id_sel]["nombre"] = limpio
                guardar_estructura(estructura)
                st.success("Nombre de la minera actualizado ✅")
                st.rerun()
            else:
                st.warning("El nombre no puede estar vacío.")

minera_id = st.session_state.get("minera_id")
if minera_id is None or minera_id not in estructura:
    st.stop()

minera_nombre = estructura[minera_id]["nombre"]
estructura[minera_id].setdefault("procesos", {})

st.markdown("---")

# ============================================================================
# NIVEL 2: PROCESO (dentro de la minera activa)
# ============================================================================
st.subheader(f"⚙️ Proceso — {minera_nombre}")

procesos = estructura[minera_id]["procesos"]
nombres_procesos = {pid: info["nombre"] for pid, info in procesos.items()}

col1, col2 = st.columns([2, 1])

with col1:
    if nombres_procesos:
        ids_procesos = list(nombres_procesos.keys())
        nombres_p_lista = list(nombres_procesos.values())
        idx_default = 0
        if st.session_state.get("proceso_id") in ids_procesos:
            idx_default = ids_procesos.index(st.session_state["proceso_id"])
        nombre_proceso_sel = st.selectbox(
            "Proceso activo", options=nombres_p_lista, index=idx_default, key="select_proceso"
        )
        proceso_id_sel = ids_procesos[nombres_p_lista.index(nombre_proceso_sel)]
    else:
        proceso_id_sel = None
        st.info(f"'{minera_nombre}' aún no tiene procesos. Agrega uno (ej. Proceso 001) →")

with col2:
    st.write("")
    st.write("")
    nuevo_proceso = st.text_input(
        "Agregar nuevo proceso", placeholder="Ej: Proceso 001", key="nuevo_proceso_input"
    )
    if st.button("➕ Agregar proceso", use_container_width=True):
        nombre = nuevo_proceso.strip()
        if not nombre:
            st.warning("Escribe un nombre de proceso.")
        else:
            pid = nuevo_id()
            estructura[minera_id]["procesos"][pid] = {"nombre": nombre}
            guardar_estructura(estructura)
            st.session_state.proceso_id = pid
            st.rerun()

if proceso_id_sel is not None:
    st.session_state.proceso_id = proceso_id_sel

    with st.expander("✏️ Renombrar proceso seleccionado"):
        nuevo_nombre_proceso = st.text_input(
            "Nuevo nombre", value=procesos[proceso_id_sel]["nombre"], key="rename_proceso_input"
        )
        if st.button("Guardar nuevo nombre", key="rename_proceso_btn"):
            limpio = nuevo_nombre_proceso.strip()
            if limpio:
                estructura[minera_id]["procesos"][proceso_id_sel]["nombre"] = limpio
                guardar_estructura(estructura)
                st.success("Nombre del proceso actualizado ✅")
                st.rerun()
            else:
                st.warning("El nombre no puede estar vacío.")

proceso_id = st.session_state.get("proceso_id")
if proceso_id is None or proceso_id not in procesos:
    st.stop()

proceso_nombre = procesos[proceso_id]["nombre"]

clave_actual = f"{minera_id}_{proceso_id}"
if "df" not in st.session_state or st.session_state.get("clave_datos_cargados") != clave_actual:
    st.session_state.df = cargar_datos(minera_id, proceso_id)
    st.session_state.clave_datos_cargados = clave_actual

st.caption(f"Trabajando actualmente sobre: **{minera_nombre} → {proceso_nombre}**")
st.markdown("---")

# ============================================================================
# FORMULARIO: NUEVO REGISTRO
# ============================================================================
st.subheader("📋 Nuevo Registro")

with st.form("form_registro", clear_on_submit=True):
    col1, col2 = st.columns(2)

    with col1:
        fecha = st.date_input("Fecha", value=date.today())
        tanque_select = st.selectbox("Tanque", options=TANQUE_OPTIONS)
        tanque_manual = st.text_input("O escribe otro tanque (opcional)", placeholder="Ej: D1")
        volumen = st.selectbox("Volumen (t)", options=VOLUMEN_OPTIONS)
        ley_cabeza = st.number_input("Ley Cabeza (g/t)", min_value=0.0, step=0.01, format="%.2f")

    with col2:
        ley_cola = st.number_input("Ley Cola (g/t)", min_value=0.0, step=0.01, format="%.2f")
        cianuro = st.selectbox("Cianuro (kg)", options=CIANURO_OPTIONS)
        cal = st.selectbox("Cal (fundas)", options=CAL_OPTIONS, format_func=lambda x: f"{x:.2f}")

    submitted = st.form_submit_button("💾 Guardar Registro", use_container_width=True)

    if submitted:
        tanque = tanque_manual.strip() if tanque_manual.strip() else tanque_select
        if not tanque:
            st.error("El campo 'Tanque' es obligatorio.")
        else:
            oro_recuperado = volumen * (ley_cabeza - ley_cola)
            nuevo = pd.DataFrame([{
                "Fecha": pd.to_datetime(fecha),
                "Tanque": tanque,
                "Volumen": volumen,
                "Ley Cabeza": ley_cabeza,
                "Ley Cola": ley_cola,
                "Cianuro": cianuro,
                "Cal (fundas)": cal,
                "Oro Recuperado (g)": round(oro_recuperado, 2),
            }])
            st.session_state.df = pd.concat([st.session_state.df, nuevo], ignore_index=True)
            guardar_datos(st.session_state.df, minera_id, proceso_id)
            st.success(f"Registro del tanque {tanque} guardado en {minera_nombre} → {proceso_nombre} ✅")

st.markdown("---")

# ============================================================================
# RESUMEN DEL DÍA
# ============================================================================
st.subheader("📊 Resumen del día")

fecha_filtro = st.date_input("Ver resumen de la fecha:", value=date.today(), key="filtro_fecha")

df = st.session_state.df.copy()
if not df.empty:
    df["Fecha"] = pd.to_datetime(df["Fecha"])
    df_dia = df[df["Fecha"].dt.date == fecha_filtro]
else:
    df_dia = df

col1, col2, col3, col4 = st.columns(4)
col1.metric("Tanques", int(df_dia.shape[0]))
col2.metric("Oro Recuperado", f'{df_dia["Oro Recuperado (g)"].sum():.2f} g')
col3.metric("Cianuro", f'{df_dia["Cianuro"].sum():.2f} kg')
col4.metric("Cal", f'{df_dia["Cal (fundas)"].sum():.2f} fundas')

st.markdown("---")

# ============================================================================
# RESUMEN TOTAL
# ============================================================================
st.subheader("📈 Resumen Total")

col1, col2, col3, col4 = st.columns(4)
col1.metric("Tanques", int(df.shape[0]))
col2.metric("Oro Recuperado", f'{df["Oro Recuperado (g)"].sum():.2f} g' if not df.empty else "0.00 g")
col3.metric("Cianuro", f'{df["Cianuro"].sum():.2f} kg' if not df.empty else "0.00 kg")
col4.metric("Cal", f'{df["Cal (fundas)"].sum():.2f} fundas' if not df.empty else "0.00 fundas")

st.markdown("---")

# ============================================================================
# TABLA DE REGISTROS DEL DÍA
# ============================================================================
st.subheader("🗂️ Registros")

if df_dia.empty:
    st.info("No hay registros para la fecha seleccionada.")
else:
    st.dataframe(df_dia, use_container_width=True, hide_index=True)

# ============================================================================
# EDITAR / ELIMINAR REGISTROS HISTÓRICOS
# ============================================================================
st.markdown("---")
st.subheader("✏️ Editar / Eliminar Registros")

if df.empty:
    st.info("Aún no hay registros guardados para editar.")
else:
    st.caption(
        "Haz doble clic en una celda para editarla. Para eliminar un registro, "
        "selecciona la fila (checkbox o número a la izquierda) y presiona la tecla "
        "Supr/Delete, o usa el ícono de la papelera."
    )
    df_editado = st.data_editor(
        df,
        use_container_width=True,
        hide_index=True,
        num_rows="dynamic",
        key="editor_registros",
        column_config={
            "Fecha": st.column_config.DateColumn("Fecha"),
            "Tanque": st.column_config.SelectboxColumn("Tanque", options=TANQUE_OPTIONS + ["Otro"]),
            "Volumen": st.column_config.NumberColumn("Volumen (t)", format="%.2f"),
            "Ley Cabeza": st.column_config.NumberColumn("Ley Cabeza (g/t)", format="%.2f"),
            "Ley Cola": st.column_config.NumberColumn("Ley Cola (g/t)", format="%.2f"),
            "Cianuro": st.column_config.NumberColumn("Cianuro (kg)", format="%.2f"),
            "Cal (fundas)": st.column_config.NumberColumn("Cal (fundas)", format="%.2f"),
            "Oro Recuperado (g)": st.column_config.NumberColumn("Oro Recuperado (g)", format="%.2f"),
        },
    )

    col_a, col_b = st.columns([1, 3])
    with col_a:
        guardar_cambios = st.button("💾 Guardar cambios", use_container_width=True)
    with col_b:
        st.caption(f"Los cambios se guardan en **{minera_nombre} → {proceso_nombre}**.")

    if guardar_cambios:
        df_editado = df_editado.copy()
        df_editado["Oro Recuperado (g)"] = (
            df_editado["Volumen"] * (df_editado["Ley Cabeza"] - df_editado["Ley Cola"])
        ).round(2)
        st.session_state.df = df_editado.reset_index(drop=True)
        guardar_datos(st.session_state.df, minera_id, proceso_id)
        st.success("Cambios guardados correctamente ✅")
        st.rerun()

# ============================================================================
# DESCARGA DE HISTORIAL
# ============================================================================
with st.expander("Ver / descargar historial completo"):
    if df.empty:
        st.info("Aún no hay registros guardados.")
    else:
        st.dataframe(df, use_container_width=True, hide_index=True)
        csv = df.to_csv(index=False).encode("utf-8")
        st.download_button(
            "⬇️ Descargar historial (CSV)",
            data=csv,
            file_name=f"historial_{minera_nombre}_{proceso_nombre}.csv".replace(" ", "_"),
            mime="text/csv",
        )
