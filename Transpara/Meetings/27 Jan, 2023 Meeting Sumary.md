
- tCores are not going to be related to interfaces now
- **JUST ONE** tMon and tBackup
- We need to understand the codebase of tSystem

**Step 1**: Get a blank tSystem manually installed from Dockerfiles
**Step 2**: Start by doing a tStore installation
**Step 3**: Create a V6 developing branch

---

![[Borg Architecture.pdf]]

---
## Miguel's Notes:

Conclusiones:

1.  clonar el repo tsystem
2.  crear una branch nueva quizas llamada "V6-develop" tomando como base la rama "master"
3.  clonar el repo deployment, y para hacer la instalación manual únicamente de tSystem, entonces usar solo el docker-compose de tsystem
4.  construir (build) una imagen de tsystem tomando como base la rama "V6-develop" recientemente creada, y ponerle como tag 1.0.0
5.  modificar el docker-compose de tsystem (localmente) y poner la tag que hemos creado, 
6.  docker-compose up
7.  ver si funcionó o tuvimos problemas porque seguramente tsystem es actualmente dependiente de tstore

#meeting 