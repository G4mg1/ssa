import discord
from discord import app_commands
from discord.ext import commands

TOKEN = "MTQ0MjU3NjY3OTE2MjYxMzgyMA.GqwOK_.bMeVndZZrPM39LGNYIDLlXqGHkA-DESRokxmuc" 

intents = discord.Intents.default()
bot = commands.Bot(command_prefix="!", intents=intents)

@bot.event
async def on_ready():
    print(f"Logged in as {bot.user}")
    try:
        await bot.tree.sync()
        print("Slash commands synced.")
    except Exception as e:
        print(e)

@bot.tree.command(name="saysomething", description="Say something and the bot repeats it.")
@app_commands.describe(text="Type something for the bot to return")
async def saysomething(interaction: discord.Interaction, text: str):
    # Returns ONLY the player's response
    await interaction.response.send_message(text)

bot.run(TOKEN)
