# BotSafe
import os
import discord
from discord.ext import commands

client = commands.Bot(command_prefix='!', case_insensitive=True)

bad_words = ['porra', 'viadinho', 'buceta'] # adicione aqui as palavras que você deseja bloquear

@client.event
async def on_ready():
    print(f'{client.user} está conectado ao Discord!')

@client.event
async def on_message(message):
    if message.author == client.user or message.content == "":
        return
    for word in bad_words:
        if message.content.lower().startswith(word):
            await message.delete()
            await message.channel.send(f'{message.author.mention}, por favor, evite usar palavras pejorativas ou xingamentos neste servidor.')
            break
    await client.process_commands(message)

client.run(os.environ['MTEwMzA1MDU3MzQ0OTc4OTUwMQ.Gcml40.MJ9oXlAfh6jJMEcn-jY18Xz6lZOn4XecdM4S8g']) # não se esqueça de configurar a variável de ambiente com o token do seu bot
