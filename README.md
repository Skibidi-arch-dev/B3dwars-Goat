package com.example.bedwars;

import org.bukkit.Bukkit;
import org.bukkit.Location;
import org.bukkit.Material;
import org.bukkit.plugin.java.JavaPlugin;
import org.bukkit.entity.Player;
import org.bukkit.event.Listener;
import org.bukkit.event.EventHandler;
import org.bukkit.event.player.PlayerRespawnEvent;
import org.bukkit.event.player.PlayerInteractEvent;
import org.bukkit.event.block.BlockBreakEvent;
import org.bukkit.block.Block;

public class BedwarsMain extends JavaPlugin implements Listener {

    private Location bedLocation;

    @Override
    public void onEnable() {
        // Example bed location, change to your world and coordinates
        bedLocation = new Location(Bukkit.getWorld("world"), 100, 64, 100);
        Bukkit.getPluginManager().registerEvents(this, this);
        getLogger().info("Bedwars plugin enabled!");
    }

    @EventHandler
    public void onPlayerRespawn(PlayerRespawnEvent event) {
        // Respawn player at spawn or bed location
        event.setRespawnLocation(bedLocation);
    }

    @EventHandler
    public void onBlockBreak(BlockBreakEvent event) {
        Block block = event.getBlock();
        if (block.getType() == Material.BED) {
            // Handle bed destroyed
            event.getPlayer().sendMessage("You broke the bed! That team can no longer respawn!");
            // Add your team elimination logic here
        }
    }

    @EventHandler
    public void onPlayerInteract(PlayerInteractEvent event) {
        // Add shop, resource generator, or other interactions here
    }
}
