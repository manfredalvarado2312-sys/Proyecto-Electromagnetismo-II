# Visualización Computacional de un Dipolo Eléctrico Oscilante

**Curso:** FS0820 Electromagnetismo II  
**Profesora:** Marcela Hernández Jiménez
**Estudiantes:** Manfred Alvarado López (10318) / Anaité Chaves Ramirez (C12154)  
**Semestre:** II-2026 

---

## 1. Descripción del Proyecto
Este repositorio contiene las herramientas de programación y visualización desarrolladas para estudiar la estructura espacial y temporal de los campos electromagnéticos $\mathbf{E}(\mathbf{r}, t)$ y $\mathbf{B}(\mathbf{r}, t)$, así como el transporte de energía mediante el vector de Poynting $\mathbf{S}(\mathbf{r}, t)$, producidos por un dipolo eléctrico puntual localizado en el origen que oscila armónicamente en la dirección $\hat{\mathbf{z}}$:

$$\mathbf{p}(t) = p_0 \cos(\omega t)\,\hat{\mathbf{z}}$$

A partir de las soluciones analíticas exactas en el calibre de Lorenz (Griffiths, 4ta ed., Cap. 10 y Cap. 11), el código permite explorar la transición física entre tres regímenes espaciales en función de la longitud de onda $\lambda = 2\pi c / \omega$:
* **Región cercana (cuasiestática / inducción):** $r \ll \lambda$
* **Región intermedia (zona de transición):** $r \sim \frac{\lambda}{2\pi}$ ($kr \sim 1$)
* **Región lejana (zona de radiación):** $r \gg \lambda$

---

## 2. Estructura del Notebook (`proyecto_visualizacion.ipynb`)
El código trabaja en unidades adimensionales ($\lambda = 1$, $T = 1$, de modo que $k = 2\pi$ y $\omega = 2\pi$) y está modularizado en las siguientes funciones principales:

* **`calcular_campos_dipolo(X, Z, t=0.0, terminos=('1/r3', '1/r2', '1/r'))`**: Motor físico que evalúa analíticamente las componentes esféricas y cartesianas de $\mathbf{E}$, $\mathbf{B}$, el vector de Poynting instantáneo $\mathbf{S}(t)$ y el promedio temporal exacto $\langle\mathbf{S}\rangle$ en el plano $xz$. Permite activar o desactivar selectivamente las contribuciones radiales $1/r^3$, $1/r^2$ y $1/r$.
* **`perfil_radial(...)`**: Grafica en escala log-log el decaimiento radial de las amplitudes de $|E_r|$, $|E_\theta|$ y $c|B_\phi|$, verificando numéricamente las pendientes asintóticas en las zonas cercana ($r^{-3}$, $r^{-2}$) y de radiación ($r^{-1}$).
* **`explorar_regimen(...)`**: Genera paneles comparativos de $\log_{10}|\mathbf{E}|$ (con líneas de campo), $\log_{10}(c|B_\phi|)$ (con contornos nodales) y líneas de flujo de $\mathbf{S}(t)$ a través de los distintos regímenes espaciales, permitiendo usar una escala de color común o independiente.
* **`orientacion_radiacion(...)`**: Visualiza mediante mapas de vectores (`quiver`) y perfiles radiales la ortogonalidad mutua entre $\mathbf{E}$, $\mathbf{B}$ y la dirección de propagación $\hat{\mathbf{r}}$, verificando que $E_\theta$ y $cB_\phi$ oscilan en fase en la zona lejana.
* **`poynting_promedio(...)`**: Representa el flujo neto de energía $\langle\mathbf{S}\rangle$ y compara cuantitativamente la magnitud y dirección del vector de Poynting instantáneo frente a su promedio temporal tanto en la región cercana como en la de radiación.
* **`patron_angular(...)`**: Grafica el diagrama polar y cartesiano de la distribución angular de potencia radiada $dP/d\Omega \propto \sin^2\theta$ y reporta los valores relativos en direcciones características.
* **`perfil_radial_3d(...)`**: Genera superficies tridimensionales de la evolución espacio-temporal de los campos en función de $r/\lambda$ y $t/T$.

---

## 3. Requisitos y Ejecución
Para ejecutar correctamente el notebook se requiere **Python 3.8+** y las siguientes bibliotecas estándar de computación científica:

```bash
pip install numpy matplotlib jupyter
