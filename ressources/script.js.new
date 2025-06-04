document.addEventListener('DOMContentLoaded', function() {
    // Fonction pour activer le lien de navigation correspondant à la section visible
    function activerLienNavigation(targetId) {
        // Désactiver tous les liens actifs dans le menu principal et mobile
        document.querySelectorAll('.lienMenu, .lienMenuMobile').forEach(lien => {
            lien.classList.remove('actif');
        });
        
        // Activer les liens correspondants à la section cible
        setTimeout(() => {
            document.querySelectorAll(`.lienMenu[href="${targetId}"], .lienMenuMobile[href="${targetId}"]`).forEach(lien => {
                lien.classList.add('actif');
            });
        }, 10); // Petit délai pour permettre à la transition CSS de se réinitialiser
    }
    
    // Activer le lien Accueil par défaut au chargement de la page
    activerLienNavigation('#accueil');
    
    // Gestion de l'effet de défilement sur la barre de navigation
    const navigation = document.querySelector('.navigation');
    
    window.addEventListener('scroll', function() {
        if (window.scrollY > 50) {
            navigation.classList.add('navigation-scrolled');
        } else {
            navigation.classList.remove('navigation-scrolled');
        }
    });
    
    // Gestion de l'animation du sélecteur
    const selectElements = document.querySelectorAll('select');
    
    selectElements.forEach(select => {
        // Ajouter la classe lors de l'ouverture du select
        select.addEventListener('mousedown', function() {
            // On ajoute un délai pour que la classe soit ajoutée après l'ouverture du menu
            setTimeout(() => {
                this.classList.add('select-open');
            }, 10);
        });
        
        // Retirer la classe lorsque le select perd le focus
        select.addEventListener('blur', function() {
            this.classList.remove('select-open');
        });
        
        // Retirer la classe après la sélection d'une option
        select.addEventListener('change', function() {
            this.classList.remove('select-open');
        });
    });
    
    // Animation au scroll avec Intersection Observer
    const observerOptions = {
        root: null, // utilise le viewport comme conteneur
        rootMargin: '0px',
        threshold: 0.15 // déclenche quand 15% de l'élément est visible
    };
    
    const animationObserver = new IntersectionObserver(function(entries, observer) {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add('animation-visible');
                observer.unobserve(entry.target); // arrête d'observer une fois animé
            }
        });
    }, observerOptions);
    
    // Sélectionne tous les éléments avec une classe d'animation
    document.querySelectorAll('.animation-fade-up, .animation-fade-left, .animation-fade-right, .animation-scale').forEach(element => {
        animationObserver.observe(element);
    });
    
    // Gestion du menu mobile
    const boutonMenuMobile = document.getElementById('boutonMenuMobile');
    const menuMobileConteneur = document.getElementById('menuMobileConteneur');
    const fermerMenuMobile = document.getElementById('fermerMenuMobile');
    const menuMobileOverlay = document.getElementById('menuMobileOverlay');
    
    // Fonction pour ouvrir le menu mobile
    function ouvrirMenuMobile() {
        menuMobileConteneur.classList.add('actif');
        menuMobileOverlay.classList.add('actif');
        document.body.style.overflow = 'hidden'; // Empêche le défilement de la page
    }
    
    // Fonction pour fermer le menu mobile
    function fermerMenu() {
        menuMobileConteneur.classList.remove('actif');
        menuMobileOverlay.classList.remove('actif');
        document.body.style.overflow = ''; // Réactive le défilement de la page
    }
    
    // Événement pour ouvrir le menu
    if (boutonMenuMobile && menuMobileConteneur) {
        boutonMenuMobile.addEventListener('click', ouvrirMenuMobile);
    }
    
    // Événement pour fermer le menu avec le bouton X
    if (fermerMenuMobile) {
        fermerMenuMobile.addEventListener('click', fermerMenu);
    }
    
    // Événement pour fermer le menu en cliquant sur l'overlay
    if (menuMobileOverlay) {
        menuMobileOverlay.addEventListener('click', fermerMenu);
    }
    
    // Fermer le menu en cliquant sur un lien du menu
    const liensMenuMobile = document.querySelectorAll('.lienMenuMobile');
    liensMenuMobile.forEach(lien => {
        lien.addEventListener('click', fermerMenu);
    });
    
    // Gestion des questions FAQ
    const faqQuestions = document.querySelectorAll('.faqQuestion');
    
    faqQuestions.forEach(question => {
        question.addEventListener('click', function() {
            // Récupère l'élément parent (faqItem)
            const faqItem = this.parentElement;
            
            // Toggle la classe 'actif' sur l'élément parent
            faqItem.classList.toggle('actif');
            
            // Si on veut fermer les autres questions quand on en ouvre une
            if (faqItem.classList.contains('actif')) {
                faqQuestions.forEach(q => {
                    if (q !== this) {
                        q.parentElement.classList.remove('actif');
                    }
                });
            }
        });
    });
    
    // Gestion du formulaire de démo
    const formulaireDemo = document.getElementById('formulaireDemo');
    
    if (formulaireDemo) {
        formulaireDemo.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Récupération des valeurs du formulaire
            const nomComplet = document.getElementById('nomComplet').value;
            const telephone = document.getElementById('telephone').value;
            const fonction = document.getElementById('fonction').value;
            const question = document.getElementById('question').value;
            
            // Validation simple
            if (!nomComplet || !telephone || !fonction) {
                alert('Veuillez remplir tous les champs obligatoires.');
                return;
            }
            
            // Ici, vous pourriez envoyer les données à un serveur
            // Pour cette démo, nous affichons simplement un message de confirmation dynamique
            
            // Créer un élément de confirmation
            const confirmation = document.createElement('div');
            confirmation.className = 'confirmationDemo';
            confirmation.innerHTML = `
                <div class="confirmationContenu">
                    <div class="confirmationIcone">
                        <img src="ressources/icone/check.svg" alt="Succès">
                    </div>
                    <h3>Merci pour votre demande !</h3>
                    <p>Nous avons bien reçu votre demande de démonstration. Un membre de notre équipe vous contactera très prochainement.</p>
                </div>
            `;
            
            // Remplacer le formulaire par le message de confirmation
            formulaireDemo.parentNode.replaceChild(confirmation, formulaireDemo);
            
            // Animation du message de confirmation
            setTimeout(() => {
                confirmation.style.opacity = '1';
                confirmation.querySelector('.confirmationIcone').style.animation = 'scaleIn 0.5s ease forwards';
                confirmation.querySelector('h3').style.animation = 'fadeIn 0.5s ease forwards';
                confirmation.querySelector('p').style.animation = 'fadeIn 0.7s ease forwards';
            }, 100);
        });
    }
    
    // Détecter la section visible lors du défilement
    function detecterSectionVisible() {
        // Obtenir toutes les sections avec un ID
        const sections = document.querySelectorAll('section[id]');
        
        // Vérifier si nous sommes tout en haut de la page
        if (window.scrollY < 100) {
            // Si nous sommes en haut de la page, activer le lien Accueil
            activerLienNavigation('#accueil');
            return;
        }
        
        // Trouver la section la plus proche du haut de la fenêtre
        let sectionActive = null;
        let minDistance = Infinity;
        
        sections.forEach(section => {
            const rect = section.getBoundingClientRect();
            const distance = Math.abs(rect.top - 100); // 100px de décalage pour tenir compte du header
            
            if (distance < minDistance) {
                minDistance = distance;
                sectionActive = section;
            }
        });
        
        // Si une section est trouvée, activer le lien correspondant
        if (sectionActive) {
            activerLienNavigation('#' + sectionActive.id);
        } else {
            // Si aucune section n'est visible, activer le lien Accueil par défaut
            activerLienNavigation('#accueil');
        }
    }
    
    // Écouter l'événement de défilement avec throttling pour les performances
    let scrollTimeout;
    window.addEventListener('scroll', function() {
        if (!scrollTimeout) {
            scrollTimeout = setTimeout(function() {
                detecterSectionVisible();
                scrollTimeout = null;
            }, 100); // Limiter à une exécution toutes les 100ms
        }
    });
    
    // Initialiser la navigation active au chargement de la page
    detecterSectionVisible();
    
    // Gestion des liens d'ancrage pour une navigation fluide
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
        anchor.addEventListener('click', function(e) {
            const targetId = this.getAttribute('href');
            
            // Si l'ancre pointe vers une section existante
            if (targetId !== '#' && document.querySelector(targetId)) {
                e.preventDefault();
                
                // Activer le lien correspondant
                activerLienNavigation(targetId);
                
                const targetElement = document.querySelector(targetId);
                window.scrollTo({
                    top: targetElement.offsetTop - 80, // Ajustement pour la barre de navigation
                    behavior: 'smooth'
                });
                
                // Fermer le menu mobile si ouvert
                if (menuMobileConteneur && menuMobileConteneur.classList.contains('actif')) {
                    menuMobileConteneur.classList.remove('actif');
                    menuMobileOverlay.classList.remove('actif');
                }
            }
        });
    });
});
