Porting RailCraft
=================
Needed tools and files
----------------------
To port RailCraft, you need the following:
(Note: most of these are already in this git repository)

  - [ApplySrg.jar]
  - Valid [vanilla to bukkit mappings] for the Minecraft version you're porting on.
  - [ObjectWeb's ASM toolkit]
  - A vanilla minecraft_server.jar, obviously the version you're porting on.

Step 1: Applying the SRG mapping
--------------------------------
To apply the SRG mapping, we use ApplySrg.jar. Apart from which mappings to use, we also need it to build an inheritance tree to help with the mapping, and because sometimes classes expect to be in the same package as Minecraft, we need to specify the package for orphan classes too:
> java -jar ../bin/ApplySrg.jar --inheritance "minecraft_server.jar" --inheritance "Railcraft_Server_5.0.3.zip" --srg "../mappings/server_vanilla_bukkit_1.2.5.srg" --in "Railcraft_Server_5.0.3.zip" --out "Step2.zip"

Step 2: Applying fixes
----------------------
Due to a couple of changes in Bukkit from the vanilla minecraft server, we sometimes need to patch things up a little. Luckily in RailCraft, these patches can be easily automated.
In this case they are automated with ObjectWeb's ASM toolkit and XSL mappings, but in other cases you could also decompile or disassemble, apply patches, and then recompile or reassemble.

For railcraft, the following command will apply the patches:
> java -classpath ../bin/asm-all-3.3.1.jar org.objectweb.asm.xml.Processor code code -in "Step2.zip" -out "Railcraft_Server_5.0.3_Bukkit.zip" -xsl "fixRailCraft.xsl"


  [ApplySrg.jar]: https://github.com/Frans-Willem/ApplySrg
  [vanilla to bukkit mappings]: https://github.com/Frans-Willem/MinecraftMappings
  [ObjectWeb's ASM toolkit]: file:///D:/Users/Frans-Willem/Downloads/asm-3.3.1-bin.zip
