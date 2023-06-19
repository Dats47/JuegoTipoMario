#include <SFML/Graphics.hpp>
#include <iostream>

// Función para mover al jugador
void MoverJugador(float& jugadorX, float& jugadorY, float desplazamientoX, float desplazamientoY, float deltaTime)
{
    // Calcular la nueva posición del jugador
    float nuevaPosX = jugadorX + desplazamientoX * deltaTime;
    float nuevaPosY = jugadorY + desplazamientoY * deltaTime;

    // Actualizar las coordenadas del jugador
    jugadorX = nuevaPosX;
    jugadorY = nuevaPosY;
}

// Función para actualizar la posición del jugador en el sprite
void ActualizarPosicionJugador(sf::Sprite& jugador, float jugadorX, float jugadorY)
{
    jugador.setPosition(jugadorX, jugadorY);
}

int main()
{
    sf::RenderWindow ventana(sf::VideoMode(800, 600), "Mario Bros");

    // Cargar la textura del jugador
    sf::Texture texturaJugador;
    if (!texturaJugador.loadFromFile("personaje.png")) {
        std::cout << "Error al cargar la textura del jugador." << std::endl;
        return -1;
    }

    // Crear el sprite del jugador y configurar su posición y escala
    sf::Sprite jugador;
    jugador.setTexture(texturaJugador);
    jugador.setScale(0.5f, 0.5f);
    jugador.setPosition(0.0f, 350.0f);

    // Crear el fondo y la plataforma
    sf::RectangleShape fondo(sf::Vector2f(800.0f, 600.0f));
    fondo.setFillColor(sf::Color::Blue);

    sf::RectangleShape plataforma(sf::Vector2f(800.0f, 200.0f));
    plataforma.setFillColor(sf::Color::Green);
    plataforma.setPosition(0.0f, 400.0f);

    // Variables de control del jugador
    float jugadorX = 0.0f;
    float jugadorY = 350.0f;
    float velocidadMovimiento = 200.0f;
    float velocidadSalto = -4600.0f; // Ajustar la velocidad de salto para elevarse más
    float gravedad = 10500.0f; // Ajustar la gravedad para caer más rápido
    bool enElAire = false;

    sf::Clock reloj;

    while (ventana.isOpen())
    {
        sf::Event evento;
        while (ventana.pollEvent(evento))
        {
            if (evento.type == sf::Event::Closed)
                ventana.close();
        }

        // Calcular el deltaTime para el movimiento suave
        float deltaTime = reloj.restart().asSeconds();

        float desplazamientoX = 0.0f;
        float desplazamientoY = 0.0f;

        // Comprobar las teclas presionadas para el movimiento horizontal
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::A))
        {
            desplazamientoX -= velocidadMovimiento;
        }
        else if (sf::Keyboard::isKeyPressed(sf::Keyboard::D))
        {
            desplazamientoX += velocidadMovimiento;
        }

        // Comprobar la tecla de espacio para el salto
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::Space) && !enElAire)
        {
            desplazamientoY = velocidadSalto;
            enElAire = true;
        }

        // Aplicar la gravedad si el jugador está en el aire
        if (enElAire)
        {
            desplazamientoY += gravedad * deltaTime;
        }

        // Mover al jugador utilizando la función personalizada
        MoverJugador(jugadorX, jugadorY, desplazamientoX, desplazamientoY, deltaTime);

        // Actualizar la posición vertical del jugador
        jugadorY += desplazamientoY * deltaTime;

        // Restringir la posición del jugador para que no caiga más abajo de la plataforma
        if (jugadorY >= 350.0f)
        {
            jugadorY = 350.0f;
            enElAire = false;
        }

        ventana.clear();
        ventana.draw(fondo);
        ventana.draw(plataforma);

        // Actualizar la posición del sprite del jugador
        ActualizarPosicionJugador(jugador, jugadorX, jugadorY);
        ventana.draw(jugador);

        ventana.display();
    }

    return 0;
}
