from aiogram import Bot, Dispatcher, types
from aiogram.utils import executor
from aiogram.types import InlineKeyboardMarkup, InlineKeyboardButton
from aiogram.dispatcher import FSMContext
from aiogram.contrib.fsm_storage.memory import MemoryStorage

import asyncio

# Token do seu bot (substitua pelo token fornecido)
TOKEN = "7653489802:AAHehe68Pu7TYfWn6m-MnCj7dY3OJLkdmZg"

# Inicializa o bot e o dispatcher
bot = Bot(token=TOKEN)
storage = MemoryStorage()
dp = Dispatcher(bot, storage=storage)

# Dados dos cursos
cursos = {
    "Matemática": {
        "Xeque Mate 2024": "https://t.me/c/2356612316/36363",
        "Matemática Online": "https://t.me/c/2356612316/35175",
        "Matemática Criativa: Extensivo 2024": "https://t.me/c/2356612316/51596",
        "Matemática Mastigada": "https://t.me/c/2356612316/43313",
        "PVO - Matemática": "https://t.me/c/2356612316/41260",
        "Mente Matemática - Treinamento 2024": "https://t.me/c/2356612316/19282",
    },
    "Natureza": {
        "Biologia": {
            "Guilherme Goulart 2024": "https://t.me/c/2356612316/37770",
            "Ramon Gadelha 2024": "https://t.me/c/2356612316/39271",
            "Medestuda": "https://t.me/c/2356612316/23189",
            "Extensivo de Biologia": "https://t.me/c/2356612316/37770",
            "Gordinho das Aprovações 2024": "https://t.me/c/2356612316/49151",
            "Biologia ProENEM": "https://t.me/c/2356612316/48288",
            "Neuralia: Extensivo Basic 2024": "https://t.me/c/2356612316/43935",
            "Discursivas de Biologia 2024": "https://t.me/c/2356612316/34021",
        },
        "Química": {
            "Curso de Química 2024 - Prof. Moisés Medeiros": "https://t.me/c/2356612316/39272",
            "IQUÍMICA 2024": "https://t.me/c/2356612316/51136",
            "Materiais de Química Discursivas": "https://abre.ai/mqdis",
            "Aprova Total Química": "https://t.me/c/2356612316/27160",
            "Discursivas de Química": "https://t.me/c/2356612316/32005",
        },
        "Física": {
            "Extensivo RedPlay 2024 - Ricci": "https://t.me/c/2356612316/49378",
            "Revisões Lições de Física - Universo Narrado": "https://t.me/c/2356612316/43098",
        },
        "PVO - Naturezas": "https://t.me/c/2356612316/40804",
    },
    "Linguagens": {
        "Redação": {
            "Jana Rabelo": "https://t.me/c/2356612316/36360",
            "Modelos e Ponto 2023": "https://t.me/c/2356612316/35874",
            "Bela Nazar 2024": "https://t.me/c/2356612316/3",
        },
        "Português": {
            "Extensivo Premium 2024": "https://t.me/c/2356612316/35873",
        },
        "Outros": {
            "Hplus Linguagens": "https://t.me/c/2356612316/53056",
            "Literatura Ferreto": "https://t.me/c/2356612316/19284",
            "Literatura Landim - Obras Literárias FUVEST Extensivo": "https://t.me/c/2356612316/53353",
            "PVO - Linguagens": "https://t.me/c/2356612316/41446",
            "Multiverso Linguagens (Lauro)": "https://t.me/c/2356612316/35478",
            "Linguagens - Fernanda Pessoa 2023": "https://t.me/c/2356612316/27154",
        },
    },
    "Humanas": {
        "História": {
            "Extensivo 2024 - Edu Morais": "https://t.me/c/2356612316/44781",
        },
        "PVO - Humanas": "https://t.me/c/2356612316/40524",
        "Humanizando": "https://t.me/c/2356612316/33547",
        "Expressões Artísticas e Literárias - FP": "https://t.me/c/2356612316/9022",
    },
    "Coleções": {
        "Vinícius Oliveira": {
            "Natureza": "https://t.me/c/2356612316/40804",
            "Matemática": "https://t.me/c/2356612316/41260",
            "Linguagens": "https://t.me/c/2356612316/41446",
            "Mentorias": "https://t.me/c/2356612316/41541",
            "Humanas": "https://t.me/c/2356612316/40524",
        },
        "Ferretto": {
            "Regionais": "https://t.me/c/2356612316/39807",
            "Discursivas 2024": "https://t.me/c/2356612316/46429",
        },
        "Aprova Total": {
            "Regionais": "https://t.me/c/2356612316/27148",
        },
    },
    "Mentorias": {
        "PVO - Mentorias": "https://t.me/c/2356612316/41541",
        "Mentorias de Exatas 2024 - Rota do Enem": "https://t.me/c/2356612316/42596",
    },
    "Outros": {
        "UERJ": "https://t.me/c/2356612316/52358",
        "Rumo à Aprovação: FUVEST & Paulistas": "https://t.me/c/2356612316/51072",
        "Materiais": "https://t.me/c/2356612316/51857",
        "Lista de Obras de Leitura Obrigatória da FUVEST 2026": "https://t.me/c/2356612316/51566",
        "800+ no Enem Vinícius Oliveira": "https://t.me/c/2356612316/29492",
        "Medestuda": "https://t.me/c/2356612316/23189",
        "Chapéu do Mago 2024": "https://t.me/c/2356612316/31201",
    },
}

# Inicia o bot
if __name__ == "__main__":
    executor.start_polling(dp, skip_updates=True)# Bot
