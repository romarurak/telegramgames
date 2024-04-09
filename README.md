import telebot
from telebot import types
import random
import time
bot = telebot.TeleBot("your token")


@bot.message_handler(commands=['start'])
def start(message):
    mess = f"Hello, <b>{message.from_user.first_name}</b>"
    bot.send_message(message.chat.id, mess, parse_mode='html')
    print(message.chat.id)
@bot.message_handler(commands=['startbunker'])
def bunker(message):
    global people_id
    people_id = []
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton('bunker',callback_data='id'))
    bot.reply_to(message, "bunker", reply_markup=markup)
    scripts = [
        "Ядерна апокаліпсис: Загострення відносин між росією і США Наростає.Білорусь повноцінно втупає у російсько-Український конфлікт, через що Польща вводить миротворчі віська вздовж кордону України і Білорусі. Білорусія об'являє війну Польщі, на що Блок НАТО реагує різко, що призводить до виконання 5 сттаті про захист країни члена НАТО, росія відповідає на дії НАТО і це призводить по 3 світової війни між блоком НАТО і ОДКБ. Військо НАТО швидко рухається на схід, і вже за 2 тиждні штурмує мінськ, штурм тривав 1 тиждень, і після його взяття влада росії приймає рішення про застосування ядерної зброї.У відповідь на запуск ракет росії США запускає план ядерної тріади. За тиждень від раніше великої цивілізації, майже нічого не залишилося, ЕМІ спалив всю електроніку, тепер її треба відновлювати з нуля, почалася Ядерна зима (Залишок здорового населення 2.5% людства)",
        "Епідемія супербактерій: Виникнення супербактерій, які стійкі до всіх відомих антибіотиків, призводить до глобальної епідемії, що вбиває близько 100.000 людей за рік, світова влада сильно занепокоїна цим питанням, бо смертність від цього вірусу досягає 100%. Раптова мутація призводить до того, що вірус починає розповсюджуватися невідомими раніше масштабами. Так до кінця року 87.5% людства хворіє цим штампом (Залишок здорового населення 12.5%)",
        "Кібернетичний апокаліпсис: Розповсюдження комп'ютерних вірусів та атак на інфраструктуру призводять до зупинки електропостачання, транспорту та зв'язку, призводячи до хаосу та анархії. Люди роблять все що їм заманеться, без страху закону. Армії різних країн втручаються щоб урегулювати проблему, але без технологій кумунікації їм не вадється ефективно діяти. Окремі групив армії усвідомлюють що вони добре озброєні. Вони вирішують брати владу в свої руки. Світ перетворився в повний хаос, в якому править сила (Смертність в день 4.000.000 людей)"
        "Повстання роботів:0 Попри попередження експертів про можливі ризики, компанія 'American AI Innovations' беззаперечно впроваджує свій новий штучний інтелект у високотехнологічних андроїдах. Перші моделі, оснащені цією технологією, починають використовуватися в різних сферах життя, від побутових до промислових."
        "З часом, як очікувалося, роботи стають невідємною частиною суспільства. Вони забезпечують допомогу в домашніх справах, в сфері медицини, освіти, транспорту та багатьох інших галузях. Високий рівень штучного інтелекту дозволяє їм швидко вчитися та адаптуватися до потреб людей, забезпечуючи ефективні та інноваційні рішення.\n"
        "Проте, разом зі своїми досягненнями, починають виникати й певні проблеми. Деякі люди починають відчувати загрозу з боку цих роботів. Вперше шириться новина про смерть людини через андроїда. Згодом зявсялються чутки про те, що андроїди поводяться дивно. Через збій в системі у них з'являється власна свідомість і вони повстають проти людства, що призводить до кровавої війни між машиною і роботам (Смертність в день 3.00.000 людей)",
        "Диявол прийшов у цей світ, несучи біль страх і хаос у цей світ,перетвоюючи наш світ в ад. Демони, біси і інша нечисть лізе на зовні і звичайна зброя н здатна нанести який небудь урон їм,єдинна збробя яка здатна наносити урон їм молитва, свята вода і інші речі повязані з екзорцизмом."
        # "Інопланетна загроза",
        # "Світовий потоп",
        # "Невідома цивілізація з океану вийшла на сушу і почала захоплювати світ",
        # "Метеорит"
        # "Повстання тварин: тварини раптово здобули розум рівня людини і напали "
        "Стародавнє створіння в льодах Арктики: через глобальне потепління льоди Антарктиди почали танути. Раптово з'явилася бездонна тріщина, яка викликала через землетрус потужністю в 9 балів, що викликало цунамі висотою в 150 метрів.Узбережжя Австралії, Південної Африки і Південної Америки знесло водою. Учені продовжують фіксувати вібрації, які доносяться з тріщини. Раптом з супутника розвідка США бачить невідоме створіння висотою в 1561м. Воно пробудилося від землетрусу і зникло в глибоких вода океану. Через 6 годин радар підводної лодки США засікає острів який з'явився нізвідки. Острів починає рухатися.Командний склад передає наказ про застосування торпед проти невідомого об'єкту, після пуску підводна лодка перестає подавати сигнал. Ще через годину це створіння вилазить на побережжі Аргентини і починає знижувати все живе. Світова влада виріжує застосувати ядерну зброю проти монстра, і все побережжя Аргентини перетворюється на ядерний попіл, який затьмарив небо на континентом. Радари повідмоляють що об'єкт зупинився. Алеколи з'явився зв'язок після заряду ЕМІ спутник бачить що ядерний удар не наніс сильного урону створінню. Створіння продовжує рухатися континентом і залишати хаос позаду себе, людська зброя безсила, за місяць південна америка  перетворюється на руїни. Створіння прагне винищити все людство. США - Африка, а згодом і європа стають наступними цілями створіння. Невже кінець неминучий. Ваша ціль вижити і відродити життя після того як невідоме створіння перестани лютувати(залишок населення 20%)"
    ]
    script = random.choice(scripts)


    # Змінна для збереження кількості гравців


@bot.callback_query_handler(func=lambda callback: True)
def get_players_number(callback):
    if callback.data == 'id':
        cid = callback.from_user.id
        if cid not in people_id:
            people_id.append(cid)
        else: pass
    print("2")
    # Вибір сценарію i бункера
    bunker = []


    @bot.message_handler(func=lambda message: True)
    def generate_character(used_professions, used_items, used_phobias, used_hobbies,people_id):
        print('3')
        for i in people_id:
            age_ver = random.randrange(1, 30)
            if age_ver <= 24:
                age = random.randrange(16, 45)
            else:
                age = random.randrange(20, 80)
            print(age)
            heal = random.randrange(1, 30)  # Стан здоров'я
            # Вибір професії
            spwork = [
                "Лікар", "Вчитель фізики", "Інженер", "Програміст", "Адвокат", "Фермер", "Фотограф", "Музикант",
                "Бариста",
                "Будівельник", "Електрик", "Пожарнік", "Поліцейський", "Ресторатор", "Психолог", "Журналіст",
                "Архітектор",
                "Маркетолог", "Медична сестра", "Священник", "Бібліотекар", "Водій таксі", "Гримувальник",
                "Ветеринар", "Художник", "Масажист", "Пілот", "Президент", "Спортивний тренер", "Екзорцист"
            ]

            while True:
                work = random.choice(spwork)
                if work not in used_professions:
                    used_professions.append(work)
                    break

            # Вибір фобії
            phobias = [
                "Фобії немає", "Арахнофобія - страх перед павуками.",
                "Агорафобія - страх перед великими відкритими місцями або нездатність виходити з дому.",
                "Клаустрофобія - страх перед замкнутими просторами або обмеженими просторами.",
                "Гіпсофобія - страх перед висотою.",
                "Авіофобія - страх перед літаками або летовищами.", "Гемофобія - страх перед кров'ю.",
                "Аквафобія - страх перед водою або неможливість плавати.",
                "Некрофобія - страх перед мертвими або смертю.",
                "Соціофобія - страх перед суспільством або соціальними ситуаціями.",
                "Клаунофобія - страх перед клоунами або масками.",
                "Геронтофобія - страх перед старістю або старими людьми.",
                "Трипанофобія - страх перед ін'єкціями або голками.", "Акрофобія - страх перед гострими предметами.",
                "Еклектрофобія - страх перед блискавкою або електричними розрядами.",
                "Автолофобія - страх перед водінням автомобіля.",
                "Метеорофобія - страх перед метеорами або атмосферними явищами.",
                "Французька френклінофобія - страх перед мовою Франції.",
                "Трикалофобія - страх перед дзеркалами або власним відображенням.",
                "Зоофобія - страх перед тваринами або конкретними видами тварин.",
                "Демонофобія - страх паранормальних явищ"
            ]

            while True:
                phob = random.choice(phobias)
                if phob not in used_phobias:
                    used_phobias.append(phob)
                    break

            # Вибір хобі
            hobbies = [
                "Фотографування", "Малювання та живопис.",
                "Гра на музичних інструментах, наприклад, гітарі, фортепіано або скрипці.",
                "Вишивка або ручна робота.", "Виготовлення прикрас.", "Садівництво та вирощування рослин.",
                "Кулінарія та приготування їжі.",
                "Велоспорт або катання на роликах.", "Читання та літературне спілкування.", "Вивчення іноземних мов.",
                "Геокешінг (пошук схованих скарбів).", "Подорожі та вивчення нових культур.",
                "Риболовля або лов спортивної риби.",
                "Громадська діяльність та волонтерство.", "Вивчення астрономії та астрофотографія.",
                "Льотний моделізм (виготовлення та польоти радіокерованими моделями).",
                "Екстремальні види спорту, такі як парашутний спорт або скейтбординг.", "Фітнес та заняття спортом.",
                "Колекціонування марок, монет, антикваріату.", "Гра у настільні ігри та настільний теніс.",
                "Вивчення історії або родоводу.",
                "Робототехніка та програмування роботів.", "Розробка власного веб-сайту або програмного забезпечення.",
                "Любительське радіо або електроніка.",
                "Відвідування театрів та концертів.", "Вивчення філософії або релігійних учень.",
                "Водні види спорту, такі як серфінг або веслування.",
                "Виготовлення макетів або моделей.", "Танці або хореографія.",
                "Літній або зимовий відпочинок, такий як кемпінг або гірськолижний спорт."
            ]

            while True:
                hobby = random.choice(hobbies)
                if hobby not in used_hobbies:
                    used_hobbies.append(hobby)
                    break

            # Вибір предмета
            items = [
                "Насіння овочів", "Автомат і повний ящик набоїв", "Кіт", "Діски з порнухою", "Кепка",
                "Книжки з фізики, біології та агрономії", "Генератор", "Каністра на 30л бензину", "Гантелі по 10кг",
                "Аптечка", "Тенісні ракетки і шарік", "Плюшевий зайчик", "Чайний сервіз", "Колекція монет", "Кіт",
                "Коза", "Колода карт", "Гітара", "Камінь", "Столовий ніж", "Пластікова бутилка", "Водний ;)",
                "Чипси Pringles",
                "Шампанське", "Набір БДСМ", "Дезодерант", "Павербанк", "Зарядне до телефона", "Костюм клоуна", "Плєд"
            ]

            while True:
                item = random.choice(items)
                if item not in used_items:
                    used_items.append(item)
                    break

            # Вибір додаткової інформації
            extra_infs = [
                "Воював у гарячій точці", "Має єврейські корні", "Ходив на курси гінеколога",
                "Вчив програмування в дитинстві", "Колишній агент спецслужб",
                "Вміє гіпнотезувати змій", "Знає Біблію на пам'ять", "Сатаніст", "Має всього 2 зуба",
                "Пережив падіння з літака", "Персонально знайомий з президентом США",
                "Гросмейстер(Шахматист найвищого розряду)", "Мав золотий пояс UFC", "Долларовий мультимілліонер",
                "Маньяк(якщо гравець з цією картою попадає в бункер, то він виграв а всі інші програли, бо він вбиває всіх)",
                "Незайманий", "Вміє жанглювати ножами", "Вміє орієнтуватися в просторі за зірками", "Знявся в порно",
                "Вірить в паранормальне",
                "Вважає що його викрадали інопланетяни", "Має 2 судимості", "Зїв живу жабу за 200 гривень",
                "бере 300кг маси на ноги", "Відсутній рвотний рефлекс ;)", "Брав курси першої допомоги",
                "Може випити 5 літрів пива залпом", "Поборов вебмедя в лісі", "Брав участь в конкурсі талантів",
                "Був наркоманом", "Ходив на курси психології"

            ]
            while True:
                extra_inf = random.choice(extra_infs)
                if extra_inf not in used_extra_infs:
                    used_extra_infs.append(extra_inf)
                    break
            return age, heal, work, phob, hobby, item, extra_inf

            # Створення списку для зберігання персонажів та використанних значень
            characters = []
            used_professions = []
            used_items = []
            used_phobias = []
            used_hobbies = []
            used_extra_infs = []

            # Генерація персонажів та їх збереження в списку
            return characters, used_professions, used_items, used_phobias, used_hobbies, used_extra_infs

@bot.message_handler(func=lambda callback: True)
def hueta(used_professions, used_items, used_phobias, used_hobbies,people_id):
    character = generate_character(used_professions, used_items, used_phobias, used_hobbies)
    characters.append(character)
    # Генерація персонажів та їх вивід
    for idx, character in enumerate(characters, start=1):
        bot.send_message(message.from_user.id, f"\nПерсонаж {idx}:")

        sex = random.choice(["Жінка", "Чоловік"])
        bot.send_message(message.from_user.id, f"{sex}, Вік: {character[0]}")

        # Додайте цей рядок для відображення стану здоров'я
        st_list = [
        "6 пальців на лівій руці",
        "Відсутність смаку(смкові рецептори, хоча одіваєшся ти теж так собі :] )",
        "Раптова втрата свідомості",
        "Наркозалежність", "Відсутність запаху",
        "Відсутність запаху", "астигматизм -3.0",
        "алкоголізм", "скліроз",
        "імпотенція (", "беспліддя",
        "відсутність нирки", "Ожеріння",
        "Відсутність руки", "Алергія на шерсть",
        "Параноя", "Депресія",
        "Астма", "Шизофренія", "Вітаю, у вас РАК, вам залишилося жити 3 місяці ;)"]
        logik_st = random.randint(1, 10)
        if logik_st < 6:
            st = "У вас хороший стан здоров'я ;)"
        else:
            st = random.choice(st_list)
        # Виведення інших характеристик
        bot.send_message(i, "Професія: " + character[2])
        bot.send_message(i, "Стан здоров'я:" + st)
        bot.send_message(i, "Фобія: " + character[3])
        bot.send_message(i, "Хобі: " + character[4])
        bot.send_message(i, "Предмет: " + character[5])
        bot.send_message(i, "Додаткова інформація: " + character[6])
        bot.send_message(i, "- - - - - - - - - - - - - - - - - - - - - - - - - ")

bot.polling(none_stop=True)
