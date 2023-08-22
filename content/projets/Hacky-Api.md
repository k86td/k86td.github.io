C'est une library écrite en Rust afin d'intéragir avec le jeux [Hackmud](https://www.hackmud.com/) . Plus spécifiquement, son API de chat.

# Premier Jet

Pour la première version, je veux uniquement que sa fonctionne. Je veux commencer à mettre en place une structure semi-logique qui vas permettre une utilisation simple et efficace. 

Donc, le but ultime est de monté un système qui permet d'analyser des messages simplement qui arrive dans ce format:
```json
{
    "ok": true,
    "chats": {
        "<username>": [
            {
                "id": "3598b8a024e394b691559a8c",
                "t": 1515984653.345,
                "from_user": "sans_comedy",
                "msg": "user joined channel",
                "is_join": true,
                "channel": "0000"
            },
            {
                "id": "5a5c170f7b97fd4315e14842",
                "t": 1515984655.629,
                "from_user": "sans_comedy",
                "msg": "its petra-fying",
                "channel": "0000"
            },
            {
                "id": "8393b5e73a021ac084090aad",
                "t": 1515984657.234,
                "from_user": "sans_comedy",
                "msg": "user left channel",
                "is_leave": true,
                "channel": "0000"
            },
            {
                "id": "8393b5e73a021ac084090aad",
                "t": 1515984660.132,
                "from_user": "com",
                "msg": "psst, this is a tell"
            },
            ...
        ],
        "<username>": []
    }
}
```

Donc on à une *HashMap* avec le nom de chaque nom d'utilisateur. Pour chacun de ceux-ci, il y a une liste d'objet qui sont les messages reçu par cet utilisateur. La façon la plus simple est de faire une boucle infinie et de quitter la boucle sur certaine condition. Dans la boucle, il serait nécessaire d'aller chercher les nouveaux messages reçu par chaque utilisateur. Ça fonctionnerais, mais ce n'est pas ce que je veux.

Il existe un pattern qui s'appelle *L'Observer Pattern*, qui permet à des classes de s'abonner à une autre classe qui enverra des événements. Lorsque ces événements sont envoyé, la classe qui envoie les événements parcourra une liste d'abonné, et appellera une fonction sur chacun d'entre eux. Je pense que sa serait une bonne idée de faire le tout ainsi. Sa permettrais de découpler les deux.

Il serait intéressant de pouvoir s'abonner à différent type d'événement. Par exemple, on pourrait avoir une classe qui s'abonne à des messages entrant pour un certain utilisateur, un autre pour des utilisateurs qui entrent/sortent d'un canal, un autre pour les messages privées. Donc une liste qui serait intéressante ressemblerait à:

1. Écouter les nouveaux messages pour un certain utilisateur
2. Écouter les nouveaux messages de *tous* les utilisateurs dans un channel spécifique
3. Écouter les nouveaux messages privée pour un utilisateur

*HackyApi* permettrais de lier le lifetime des publicateurs et écouteurs d'événements. Sinon la vie d'une dépend de l'autre, et ça peut (peut-être) occasionner des problèmes. Je ne suis pas encore investis dans Rust pour savoir. 

# References
1. [Rust Design Pattern Git](https://github.com/lpxxn/rust-design-pattern/blob/master/behavioral/observer.rs)