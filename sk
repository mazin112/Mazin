import random

import string

import telebot

# Replace 'YOUR_BOT_TOKEN' with your actual bot token obtained from BotFather

bot = telebot.TeleBot('5723010945:AAFes5mjH6Q4zWNMIGYUFBlyIjU-qFXLHT8')

@bot.message_handler(commands=['start', 'help'])

def send_welcome(message):

    bot.reply_to(message, "Welcome to the Random Code Generator Bot! Send me the number of codes you want to generate.")

@bot.message_handler(func=lambda message: True)

def generate_codes(message):

    try:

        num_codes = int(message.text)

        if num_codes <= 0:

            bot.reply_to(message, "Please enter a positive number of codes.")

        else:

            bot.reply_to(message, "Generating codes. Please wait...")

            generated_codes = []

            for _ in range(num_codes):

                code = "sk_live_" + generate_random_code(24)

                generated_codes.append(code)

            if num_codes <= 200:

                send_codes_as_message(message.chat.id, generated_codes)

            else:

                send_codes_as_file(message.chat.id, generated_codes)

    except ValueError:

        bot.reply_to(message, "Please enter a valid number.")

def generate_random_code(length):

    characters = string.ascii_letters + string.digits

    return ''.join(random.choice(characters) for _ in range(length))

def send_codes_as_message(chat_id, codes):

    bot.send_message(chat_id, "\n".join(codes))

def send_codes_as_file(chat_id, codes):

    file_content = "\n".join(codes)

    with open("generated_codes.txt", "w") as file:

        file.write(file_content)

    with open("generated_codes.txt", "rb") as file:

        bot.send_document(chat_id, file)

bot.polling()

