app.py

import streamlit as st

st.set_page_config(
    page_title="Circuit Doubt Detector AI",
    page_icon="⚡",
    layout="centered"
)

st.title("⚡ Circuit Doubt Detector AI")
st.caption("Electrical calculations made simple")

st.info(
    "Beginner educational tool. "
    "Always verify important circuit calculations."
)

mode = st.selectbox(
    "Choose a calculation",
    [
        "Ohm's Law",
        "Series Circuit",
        "Parallel Circuit"
    ]
)

st.subheader("Enter your values")

if mode == "Ohm's Law":
    voltage = st.number_input(
        "Voltage (V)", min_value=0.0, value=12.0
    )
    resistance = st.number_input(
        "Resistance (ohms)", min_value=0.0, value=6.0
    )

    if st.button("Calculate", use_container_width=True):
        if resistance == 0:
            st.error("Resistance must be greater than zero.")
        else:
            current = voltage / resistance
            st.success(f"Current = {current:.4f} A")
            st.write("Formula: I = V / R")
            st.write(
                f"I = {voltage} / {resistance} "
                f"= {current:.4f} A"
            )

            expected = st.number_input(
                "Your expected current (A)",
                min_value=0.0,
                value=2.0,
                key="ohm_expected"
            )

            if st.button("Check my answer"):
                if abs(expected - current) <= max(
                    0.01, abs(current) * 0.01
                ):
                    st.success("Correct!")
                else:
                    st.error("Mismatch. Check the calculation.")

elif mode == "Series Circuit":
    r1 = st.number_input(
        "Resistance R1 (ohms)", min_value=0.0, value=4.0
    )
    r2 = st.number_input(
        "Resistance R2 (ohms)", min_value=0.0, value=6.0
    )

    if st.button("Calculate", use_container_width=True):
        total = r1 + r2
        st.success(f"Total resistance = {total:.4f} ohms")
        st.write("Formula: Rt = R1 + R2")
        st.write(f"Rt = {r1} + {r2} = {total} ohms")

elif mode == "Parallel Circuit":
    r1 = st.number_input(
        "Resistance R1 (ohms)", min_value=0.0, value=6.0
    )
    r2 = st.number_input(
        "Resistance R2 (ohms)", min_value=0.0, value=3.0
    )

    if st.button("Calculate", use_container_width=True):
        if r1 == 0 or r2 == 0:
            st.error(
                "Enter positive resistance values "
                "greater than zero."
            )
        else:
            total = 1 / ((1 / r1) + (1 / r2))
            st.success(
                f"Equivalent resistance = {total:.4f} ohms"
            )
            st.write("Formula: 1/Rt = 1/R1 + 1/R2")
