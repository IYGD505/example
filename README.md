// adminAccess.js - Lógica de acceso de administrador
// Importante: Esta es una implementación del lado del cliente.
// No es segura para producción. Las credenciales están expuestas.

const ADMIN_EMAIL_CHECK = 'iygd505@gmail.com';
const ADMIN_PASSWORD_CHECK = 'IyGD020209'; // Contraseña en texto plano (NO USAR EN PRODUCCIÓN)

// Variable global para indicar si el administrador está autenticado
// Esto es para que otras partes del script principal puedan verificar el estado.
window.isAdminAuthenticated = false;

/**
 * Verifica las credenciales de administrador y controla la visibilidad del panel.
 */
function checkAdminAccessLogic() {
    const emailInput = document.getElementById('admin-email-input');
    const passwordInput = document.getElementById('admin-password-input');
    const loginMessage = document.getElementById('admin-login-message');
    const adminLoginArea = document.getElementById('admin-login-area');
    const adminContentArea = document.getElementById('admin-content-area');

    const email = emailInput.value.toLowerCase();
    const password = passwordInput.value;

    if (email === ADMIN_EMAIL_CHECK && password === ADMIN_PASSWORD_CHECK) {
        window.isAdminAuthenticated = true;
        adminLoginArea.classList.add('hidden');
        adminContentArea.classList.remove('hidden');
        loginMessage.classList.add('hidden'); // Ocultar mensaje de error si estaba visible
        // Llamar a renderAdminProductList si está disponible globalmente en el script principal
        if (typeof renderAdminProductList === 'function') {
            renderAdminProductList();
        }
    } else {
        window.isAdminAuthenticated = false;
        loginMessage.textContent = 'Correo electrónico o contraseña incorrectos.';
        loginMessage.classList.remove('hidden'); // Mostrar mensaje de error
    }
}

/**
 * Cierra la sesión del administrador y oculta el panel.
 */
function adminLogoutLogic() {
    window.isAdminAuthenticated = false; // Desmarcar el estado de autenticación
    const adminLoginArea = document.getElementById('admin-login-area');
    const adminContentArea = document.getElementById('admin-content-area');

    if (adminLoginArea && adminContentArea) {
        adminLoginArea.classList.remove('hidden'); // Mostrar la sección de login
        adminContentArea.classList.add('hidden');    // Ocultar el contenido de admin
        document.getElementById('admin-email-input').value = ''; // Limpiar el campo de email
        document.getElementById('admin-password-input').value = ''; // Limpiar el campo de contraseña
        document.getElementById('admin-login-message').classList.add('hidden'); // Ocultar cualquier mensaje de error
    }
    // Redirigir a la página de inicio o cualquier otra página pública
    if (typeof navigateTo === 'function') {
        navigateTo('home');
    }
}

// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getAnalytics } from "firebase/analytics";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyBkYhEtUk8nw5JgjI3BsPsbitNdhV-rV98",
  authDomain: "suci-os.firebaseapp.com",
  projectId: "suci-os",
  storageBucket: "suci-os.firebasestorage.app",
  messagingSenderId: "116626986251",
  appId: "1:116626986251:web:d9fad924762ad609173e0e",
  measurementId: "G-Y9VVX7CXRG"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const analytics = getAnalytics(app);
