import sys
from PyQt5.QtWidgets import (
    QApplication, QMainWindow, QDialog, QVBoxLayout, QHBoxLayout, QPushButton,
    QTableWidget, QTableWidgetItem, QLineEdit, QLabel, QFormLayout, QWidget, QMessageBox
)
from PyQt5.QtGui import QIcon

class LoginDialog(QDialog):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Login")
        self.usuario = None
        layout = QFormLayout()

        self.usuario_input = QLineEdit()
        self.contrasena_input = QLineEdit()
        self.contrasena_input.setEchoMode(QLineEdit.Password)
        layout.addRow("Usuario:", self.usuario_input)
        layout.addRow("Contraseña:", self.contrasena_input)

        self.boton_login = QPushButton("Iniciar Sesión")
        self.boton_login.clicked.connect(self.verificar_credenciales)
        layout.addWidget(self.boton_login)

        self.setLayout(layout)

    def verificar_credenciales(self):
        usuarios = {
            "mike12345": {"password": "lisset12345", "areas": "todas"},
            "ana_lopez": {"password": "ana12345", "areas": "ventas"},
            "luis_hernandez": {"password": "luis12345", "areas": "logistica"},
            "maria_rodriguez": {"password": "maria12345", "areas": "finanzas"},
            "carla_castillo": {"password": "carla12345", "areas": "ventas"}
        }

        usuario = self.usuario_input.text()
        contrasena = self.contrasena_input.text()

        if usuario in usuarios and usuarios[usuario]["password"] == contrasena:
            self.usuario = usuarios[usuario]
            self.accept()
        else:
            QMessageBox.critical(self, "Error", "Usuario o contraseña incorrectos")
            self.usuario_input.clear()
            self.contrasena_input.clear()

class Sistema(QMainWindow):
    def __init__(self, usuario):
        super().__init__()
        self.usuario = usuario
        self.setWindowTitle("Snacks Mike - Panel Principal")
        self.setGeometry(100, 100, 800, 600)

        layout = QVBoxLayout()

        if self.usuario["areas"] in ["todas", "productos"]:
            boton_productos = QPushButton("Gestión de Productos")
            boton_productos.setIcon(QIcon.fromTheme("folder"))
            boton_productos.clicked.connect(lambda: self.gestion("Productos", self.datos_productos))
            layout.addWidget(boton_productos)

        if self.usuario["areas"] in ["todas", "ventas"]:
            boton_ventas = QPushButton("Gestión de Ventas")
            boton_ventas.setIcon(QIcon.fromTheme("shopping-cart"))
            boton_ventas.clicked.connect(lambda: self.gestion("Ventas", self.datos_ventas))
            layout.addWidget(boton_ventas)

        if self.usuario["areas"] in ["todas", "empleados"]:
            boton_empleados = QPushButton("Gestión de Empleados")
            boton_empleados.setIcon(QIcon.fromTheme("user"))
            boton_empleados.clicked.connect(lambda: self.gestion("Empleados", self.datos_empleados))
            layout.addWidget(boton_empleados)

        if self.usuario["areas"] in ["todas", "proveedores"]:
            boton_proveedores = QPushButton("Gestión de Proveedores")
            boton_proveedores.setIcon(QIcon.fromTheme("truck"))
            boton_proveedores.clicked.connect(lambda: self.gestion("Proveedores", self.datos_proveedores))
            layout.addWidget(boton_proveedores)

        boton_cerrar_sesion = QPushButton("Cerrar Sesión")
        boton_cerrar_sesion.clicked.connect(self.cerrar_sesion)
        layout.addWidget(boton_cerrar_sesion)

        self.widget = QWidget()
        self.widget.setLayout(layout)
        self.setCentralWidget(self.widget)

        # Datos de ejemplo
        self.datos_productos = [
            {"Número": "P-001", "Nombre": "Paquete de Donas", "Tipo": "Doritos", "Precio": 30, "Stock": 50},
            {"Número": "P-002", "Nombre": "Paquete de Donas", "Tipo": "Cheetos", "Precio": 30, "Stock": 50},
            {"Número": "P-003", "Nombre": "Paquete de Donas", "Tipo": "Cheetos Flamin' Hot", "Precio": 30, "Stock": 50},
        ]
        self.datos_ventas = [
            {"Número": "V-001", "Cliente": "Carlos Pérez", "Producto": "Paquete de Donas (Doritos)", "Cantidad": 2, "Total": 60},
        ]
        self.datos_empleados = [
            {"Número": "E-001", "Nombre": "Mike", "Edad": 28, "Celular": "555-1234", "Area": "ventas", "Usuario": "mike12345", "Contraseña": "lisset12345"},
            {"Número": "E-002", "Nombre": "Ana López", "Edad": 30, "Celular": "555-2345", "Area": "ventas", "Usuario": "ana_lopez", "Contraseña": "ana12345"},
            {"Número": "E-003", "Nombre": "Luis Hernández", "Edad": 35, "Celular": "555-3456", "Area": "logistica", "Usuario": "luis_hernandez", "Contraseña": "luis12345"},
            {"Número": "E-004", "Nombre": "María Rodríguez", "Edad": 40, "Celular": "555-4567", "Area": "finanzas", "Usuario": "maria_rodriguez", "Contraseña": "maria12345"},
            {"Número": "E-005", "Nombre": "Carla Castillo", "Edad": 33, "Celular": "555-5678", "Area": "ventas", "Usuario": "carla_castillo", "Contraseña": "carla12345"}
        ]
        self.datos_proveedores = [
            {"Número": "PR-001", "Nombre": "Proveedores Cheetos", "Producto": "Cheetos", "Telefono": "555-8765"},
        ]

    def gestion(self, tabla, datos):
        # Ventana de gestión de tabla
        self.ventana_gestion = QMainWindow(self)
        self.ventana_gestion.setWindowTitle(f"Gestión de {tabla}")
        self.ventana_gestion.setGeometry(100, 100, 800, 600)

        self.tabla = QTableWidget()
        self.tabla.setColumnCount(len(datos[0]))
        self.tabla.setHorizontalHeaderLabels(datos[0].keys())
        self.tabla.setRowCount(len(datos))
        for row_idx, item in enumerate(datos):
            for col_idx, key in enumerate(item):
                self.tabla.setItem(row_idx, col_idx, QTableWidgetItem(str(item[key])))

        layout = QVBoxLayout()
        layout.addWidget(self.tabla)

        # Agregar
        if tabla == "Ventas":
            boton_agregar = QPushButton("Agregar Venta")
            boton_agregar.clicked.connect(lambda: self.agregar(tabla))
            layout.addWidget(boton_agregar)
        elif tabla == "Proveedores":
            boton_agregar = QPushButton("Agregar Proveedor")
            boton_agregar.clicked.connect(lambda: self.agregar(tabla))
            layout.addWidget(boton_agregar)
        elif tabla == "Productos":
            boton_agregar = QPushButton("Agregar Producto")
            boton_agregar.clicked.connect(lambda: self.agregar(tabla))
            layout.addWidget(boton_agregar)
        else:
            boton_agregar = QPushButton(f"Agregar {tabla[:-1]}")
            boton_agregar.clicked.connect(lambda: self.agregar(tabla))
            layout.addWidget(boton_agregar)

        # Eliminar
        boton_eliminar = QPushButton(f"Eliminar {tabla[:-1]}")
        boton_eliminar.clicked.connect(lambda: self.eliminar(tabla))
        layout.addWidget(boton_eliminar)

        # Guardar
        boton_guardar = QPushButton("Guardar Cambios")
        boton_guardar.clicked.connect(lambda: self.guardar_datos(tabla))
        layout.addWidget(boton_guardar)

        # Modificar
        boton_modificar = QPushButton("Modificar Datos")
        boton_modificar.clicked.connect(lambda: self.modificar_datos(tabla))
        layout.addWidget(boton_modificar)

        self.widget = QWidget()
        self.widget.setLayout(layout)
        self.ventana_gestion.setCentralWidget(self.widget)
        self.ventana_gestion.show()

    def agregar(self, tabla):
        # Función para agregar un nuevo registro
        if tabla == "Productos":
            dialog = QDialog(self)
            dialog.setWindowTitle("Agregar Nuevo Producto")

            layout = QFormLayout()
            numero_input = QLineEdit(dialog)
            nombre_input = QLineEdit(dialog)
            tipo_input = QLineEdit(dialog)
            precio_input = QLineEdit(dialog)
            stock_input = QLineEdit(dialog)

            layout.addRow("Número:", numero_input)
            layout.addRow("Nombre:", nombre_input)
            layout.addRow("Tipo:", tipo_input)
            layout.addRow("Precio:", precio_input)
            layout.addRow("Stock:", stock_input)

            boton_aceptar = QPushButton("Agregar", dialog)
            boton_aceptar.clicked.connect(lambda: self.agregar_producto(numero_input.text(), nombre_input.text(), tipo_input.text(), precio_input.text(), stock_input.text(), dialog))
            layout.addWidget(boton_aceptar)
            dialog.setLayout(layout)
            dialog.exec()

        elif tabla == "Ventas":
            dialog = QDialog(self)
            dialog.setWindowTitle("Agregar Venta")

            layout = QFormLayout()
            numero_input = QLineEdit(dialog)
            cliente_input = QLineEdit(dialog)
            producto_input = QLineEdit(dialog)
            cantidad_input = QLineEdit(dialog)

            layout.addRow("Número:", numero_input)
            layout.addRow("Cliente:", cliente_input)
            layout.addRow("Producto:", producto_input)
            layout.addRow("Cantidad:", cantidad_input)

            boton_aceptar = QPushButton("Agregar", dialog)
            boton_aceptar.clicked.connect(lambda: self.agregar_venta(numero_input.text(), cliente_input.text(), producto_input.text(), cantidad_input.text(), dialog))
            layout.addWidget(boton_aceptar)
            dialog.setLayout(layout)
            dialog.exec()

        elif tabla == "Proveedores":
            dialog = QDialog(self)
            dialog.setWindowTitle("Agregar Nuevo Proveedor")

            layout = QFormLayout()
            numero_input = QLineEdit(dialog)
            nombre_input = QLineEdit(dialog)
            producto_input = QLineEdit(dialog)
            telefono_input = QLineEdit(dialog)

            layout.addRow("Número:", numero_input)
            layout.addRow("Nombre:", nombre_input)
            layout.addRow("Producto:", producto_input)
            layout.addRow("Telefono:", telefono_input)

            boton_aceptar = QPushButton("Agregar", dialog)
            boton_aceptar.clicked.connect(lambda: self.agregar_proveedor(numero_input.text(), nombre_input.text(), producto_input.text(), telefono_input.text(), dialog))
            layout.addWidget(boton_aceptar)
            dialog.setLayout(layout)
            dialog.exec()

        elif tabla == "Empleados":
            dialog = QDialog(self)
            dialog.setWindowTitle("Agregar Empleado")

            layout = QFormLayout()
            numero_input = QLineEdit(dialog)
            nombre_input = QLineEdit(dialog)
            edad_input = QLineEdit(dialog)
            celular_input = QLineEdit(dialog)
            area_input = QLineEdit(dialog)
            usuario_input = QLineEdit(dialog)
            contrasena_input = QLineEdit(dialog)

            layout.addRow("Número:", numero_input)
            layout.addRow("Nombre:", nombre_input)
            layout.addRow("Edad:", edad_input)
            layout.addRow("Celular:", celular_input)
            layout.addRow("Área:", area_input)
            layout.addRow("Usuario:", usuario_input)
            layout.addRow("Contraseña:", contrasena_input)

            boton_aceptar = QPushButton("Agregar", dialog)
            boton_aceptar.clicked.connect(lambda: self.agregar_empleado(numero_input.text(), nombre_input.text(), edad_input.text(), celular_input.text(), area_input.text(), usuario_input.text(), contrasena_input.text(), dialog))
            layout.addWidget(boton_aceptar)
            dialog.setLayout(layout)
            dialog.exec()

    def agregar_producto(self, numero, nombre, tipo, precio, stock, dialog):
        if numero and nombre and tipo and precio and stock:
            nuevo_producto = {"Número": numero, "Nombre": nombre, "Tipo": tipo, "Precio": precio, "Stock": stock}
            self.datos_productos.append(nuevo_producto)
            dialog.accept()
        else:
            QMessageBox.warning(self, "Error", "Por favor complete todos los campos.")

    def agregar_venta(self, numero, cliente, producto, cantidad, dialog):
        if numero and cliente and producto and cantidad:
            total = int(cantidad) * 30  # Suponiendo precio fijo de 30 por cada venta
            nueva_venta = {"Número": numero, "Cliente": cliente, "Producto": producto, "Cantidad": cantidad, "Total": total}
            self.datos_ventas.append(nueva_venta)
            dialog.accept()
        else:
            QMessageBox.warning(self, "Error", "Por favor complete todos los campos.")

    def agregar_proveedor(self, numero, nombre, producto, telefono, dialog):
        if numero and nombre and producto and telefono:
            nuevo_proveedor = {"Número": numero, "Nombre": nombre, "Producto": producto, "Telefono": telefono}
            self.datos_proveedores.append(nuevo_proveedor)
            dialog.accept()
        else:
            QMessageBox.warning(self, "Error", "Por favor complete todos los campos.")

    def agregar_empleado(self, numero, nombre, edad, celular, area, usuario, contrasena, dialog):
        if numero and nombre and edad and celular and area and usuario and contrasena:
            nuevo_empleado = {"Número": numero, "Nombre": nombre, "Edad": edad, "Celular": celular, "Area": area, "Usuario": usuario, "Contraseña": contrasena}
            self.datos_empleados.append(nuevo_empleado)
            dialog.accept()
        else:
            QMessageBox.warning(self, "Error", "Por favor complete todos los campos.")

    def eliminar(self, tabla):
        row = self.tabla.currentRow()
        if row != -1:
            self.tabla.removeRow(row)

    def guardar_datos(self, tabla):
        pass

    def modificar_datos(self, tabla):
        pass

    def cerrar_sesion(self):
        self.close()

if __name__ == "__main__":
    app = QApplication(sys.argv)

    login_dialog = LoginDialog()
    if login_dialog.exec_() == QDialog.Accepted:
        ventana_principal = Sistema(login_dialog.usuario)
        ventana_principal.show()

    sys.exit(app.exec_())
