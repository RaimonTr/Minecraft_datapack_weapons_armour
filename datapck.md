# Datapack «op_pack» – Guía completa (Minecraft Java 1.21.x)

## CONTENIDO
1. Ubicación del mundo  
2. Creación del datapack  
3. Archivos principales  
4. Funciones de debug  
5. Pico 9×9  
6. Comando «all»  
7. Verificación  
8. Uso dentro de Minecraft  
9. Licencia GNU GPL v2 (Versión resumida)

---

# 1. UBICACIÓN DEL MUNDO

### macOS:
```
~/Library/Application Support/minecraft/saves/New World/datapacks
```

---

# 2. CREACIÓN DEL DATAPACK

### Eliminar versiones anteriores:
```
rm -rf op_pack
```

### Crear estructura correcta:
```
mkdir -p op_pack/data/minecraft/tags/function && mkdir -p op_pack/data/op_pack/function
```

### Crear pack.mcmeta:
```
cat > op_pack/pack.mcmeta << 'EOF'
{"pack":{"pack_format":48,"description":"op_pack – Kit OP + pico 9x9 + flechas explosivas (Java 1.21.x)"}}
EOF
```

### Crear load.json:
```
cat > op_pack/data/minecraft/tags/function/load.json << 'EOF'
{"values":["op_pack:arrows_tick","op_pack:debug_on_load"]}
EOF
```

---

# 3. ARCHIVOS PRINCIPALES DEL DATAPACK

## 3.1 give_kit.mcfunction
```
cat > op_pack/data/op_pack/function/give_kit.mcfunction << 'EOF'

# ESPADA NETHERITA OP
give @s netherite_sword[enchantments={sharpness:255,unbreaking:255,looting:50,sweeping_edge:10,fire_aspect:10,knockback:10,mending:1}]

# HACHA NETHERITA OP
give @s netherite_axe[enchantments={sharpness:255,efficiency:255,unbreaking:255,mending:1}]

# PICO NETHERITA OP (minado instantáneo + fortuna extrema)
give @s netherite_pickaxe[enchantments={efficiency:255,unbreaking:255,mending:1,fortune:50}]

# PICO NETHERITA 9x9 (con nombre)
give @s netherite_pickaxe[enchantments={efficiency:255,unbreaking:255,mending:1},item_name='{"text":"Pico 9x9","color":"gold","bold":true}']

# ARCO OP
give @s bow[enchantments={power:255,punch:50,flame:10,infinity:1,unbreaking:255,mending:1}]

# ARMADURA NETHERITA OP
give @s netherite_helmet[enchantments={protection:255,unbreaking:255,thorns:50,mending:1}]
give @s netherite_chestplate[enchantments={protection:255,unbreaking:255,thorns:50,mending:1}]
give @s netherite_leggings[enchantments={protection:255,unbreaking:255,thorns:50,mending:1}]
give @s netherite_boots[enchantments={protection:255,unbreaking:255,thorns:50,feather_falling:50,mending:1}]

# FLECHAS DE DAÑO EXTREMO
give @s tipped_arrow[potion_contents={custom_effects:[{id:instant_damage,duration:1,amplifier:255}]}] 64

EOF
```

---

## 3.2 arrows_tick.mcfunction
```
cat > op_pack/data/op_pack/function/arrows_tick.mcfunction << 'EOF'

# Ejecutar cada tick
schedule function op_pack:arrows_tick 1t replace

# Cualquier flecha clavada explota
execute as @e[type=arrow,nbt={inGround:1b}] at @s run summon tnt ~ ~ ~ {Fuse:0}

# Limpiar flechas clavadas
kill @e[type=arrow,nbt={inGround:1b}]

EOF
```

---

# 4. FUNCIONES DE DEBUG

### debug_on_load.mcfunction
```
cat > op_pack/data/op_pack/function/debug_on_load.mcfunction << 'EOF'
say [op_pack] Datapack cargado correctamente (Java 1.21.x)
EOF
```

### debug.mcfunction
```
cat > op_pack/data/op_pack/function/debug.mcfunction << 'EOF'
say [op_pack] DEBUG OK: Minecraft está detectando las funciones de op_pack.
EOF
```

---

# 5. PICO 9×9 (mine_9x9.mcfunction)
```
cat > op_pack/data/op_pack/function/mine_9x9.mcfunction << 'EOF'
fill ~-4 ~-4 ~-4 ~4 ~4 ~4 air replace #minecraft:mineable/pickaxe
EOF
```

---

# 6. COMANDO «all»
```
cat > op_pack/data/op_pack/function/all.mcfunction << 'EOF'
say [op_pack] Dando kit OP completo...
function op_pack:give_kit
EOF
```

---

# 7. VERIFICACIÓN DE ARCHIVOS
```
find op_pack -maxdepth 5 -type f
```

---

# 8. USO EN MINECRAFT
```
/reload
/function op_pack:debug
/function op_pack:all
/function op_pack:mine_9x9
```

---

# 9. LICENCIA GNU GPL v2 (Versión resumida)

### GNU GENERAL PUBLIC LICENSE  
Version 2, June 1991  

Se concede permiso para copiar y distribuir copias verbatim de esta licencia,  
pero no se permite modificarla.  

Este datapack se distribuye **SIN GARANTÍA ALGUNA**,  
según se indica en la sección **"NO WARRANTY"** de la licencia.  

---
