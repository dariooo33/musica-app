Elace a git: https://github.com/dariooo33/musica-app.git

# ERRORES RESUELTOS:

1.
El primer error esta en la funcion index()

all devuelve una coleccion y no puede usar paginate

Se soluciona usando otro metodo en lugar de all() como podria ser lastest():

$albums = Album::lastest()->paginate(10);


2.
El segundo error esta en update()

si el usuario registado NO es igual al usuario que subio el album O el usuario SI es admin da error 

Para cambiarlo hay que negar la verificacion de admin para que de error si NO es administador

Tambien hay que usar AND para que en caso de que sea usuario sin ser administrador no de el error. El error solo teiene que saltar al cumplirse las dos (No es el dueño ni administrador).

if (auth()->id() !== $album->user_id && !auth()->user()->isAdmin()) {
    abort(403);
}

3.
El tercer error esta en show()

Crea la varialbe $reviews pero no la debuelve, por lo que no se envia a la vista

Para corregirlo hay que añadirla al return:

return view('albums.show', compact('album', 'reviews'));