<template>
  <ion-card v-for="is in isElVisible" :key="is.id">
    <ion-card-header>
      <ion-card-title>{{ is.city }}</ion-card-title>
      <ion-button v-if="!is.status" @click="doText(true, is.id)">Подробнее</ion-button>
      <ion-button v-else="is.status" @click="doText(false, is.id)">Скрыть</ion-button>
    </ion-card-header>

    <ion-card-content v-if="is.status">
      <h1>{{ is.description }}</h1>
      <ion-card-content v-for="(imgs, index) in is.img" :key="is.id">
        <img :src="imgs">
        <h2>{{ is.title[index] }}</h2>
        <p>{{ is.description_title[index] }}</p>
        <a :href=is.link[index]>Источник</a>
      </ion-card-content>
    </ion-card-content>
  </ion-card>

  <!-- <ion-card>
    <ion-card-header>
      <ion-card-title>Березовик</ion-card-title>
      <ion-button v-if="!isElVisible" @click="doText(true)">Show</ion-button>
      <ion-button v-else="isElVisible" @click="doText(false)">Hide</ion-button>
    </ion-card-header>

    <ion-card-content v-if="isElVisible">
    </ion-card-content>
  </ion-card> -->


  <ion-card>
    <ion-card-header>
      <ion-card-title>Путевой лист</ion-card-title>
    </ion-card-header>
    <ion-card-header v-for="item in cityTask" :key="item.id">
      <ion-card-title v-if="!item.status">{{ item.title }}</ion-card-title>
      <ion-card-title v-else style="text-decoration: line-through solid !important;">{{ item.title }}</ion-card-title>
      <ion-button v-if="!item.status" @click="setDoneCity(item.id)">✔️</ion-button>
      <ion-button v-else @click="removeCity(item.id)">❌</ion-button>
    </ion-card-header>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonButton
} from '@ionic/vue'

import { ref } from 'vue'

const isElVisible = ref([
  {
    id: 0,
    status: false,
    city: 'Тейково',
    description: 'Тейково - начало маршрута',
    img: [
      '/src/components/img/img1-city1Go.jpg'
    ],
    title: [
      "Общий вид площади Ленина"
    ],
    description_title: [
      `
      Те́йково — город (с 1918) в Ивановской области России, административный центр Тейковского района, в состав которого не входит, образует городской округ Тейково. Железнодорожная станция на линии Александров — Иваново. Население — 31 305чел. (2021).

      Известен как место базирования войск РВСН. Вблизи города дислоцированы межконтинентальные баллистические ракеты, в том числе «Тополь-М» и «Ярс».
      `
    ],
    link: [
      "https://ru.ruwiki.ru/wiki/Тейково"
    ]
  },
  {
    id: 1,
    status: false,
    city: 'Березовик',
    description: 'Березовик',
    img: [
      '/src/components/img/img1-city1.jpg',
      '/src/components/img/img2-city1.jpg',
      '/src/components/img/img3-city1.jpg',
      '/src/components/img/img4-city1.jpg'

    ],
    title: [
      'Источник иконы Божией Матери «Всех Скорбящих Радость»',
      'Источник святого Архистратига Михаила',
      'Могила Парвицкого',
      'Церковь иконы Божией Матери «Всех скорбящих Радость»'
    ],
    description_title: [
      `
      Один из трёх источников, бивших когда-то из-под горы Скорбященского храма. Расположен приблизительно в 150 метрах от церкви. Сюда ведёт витиеватая тропинка, минуя некогда прекрасный парк, обоснованный местными дворянами.
      `,

      `
      В 2002 году по благословению архиепископа Иваново-Вознесенского Амвросия в селе Берёзовик на источнике была сооружена купальня. Строительство велось мастером Сергеем Юдиным на благотворительные средства предпринимателя из города Тейково Владимира Киселёва. В 2014 году она пришла в ветхость и была разобрана.

      В этом же году на средства благотворительницы из Тейкова Альбины Владимировой возводится новая купальня. Проект и плотницкие работы выполнены мастером Сергеем Юдиным. Активное участие в строительстве принимали Олег Устяг и Александр Селиверстов, посетители источника из Тейкова. Работы по подведению воды и дренажной системы организованы прихожанами храма во главе с Сергеем Садовниковым. Освящение произошло 6 ноября 2014 года благочинным протоиереем Павлом Пономарёвым.

      В 2015 году на месте первой купальни воздвигнута надкладезная сень для набора воды посетителями сего святого места. Струя воды проходит через отверстие в установленном здесь гранитном кресте.
      `,

      `
      Любовь, взаимное уважение, чувство долга – всё то, что вызывает ассоциации с понятием     нравственности,    достигает  апогея  именно в браке,  скреплённом семейными узами.

      Коснёмся имён тех, чья  любовная коллизия предстанет перед нами в эпистолярном наследии    семейств      Каретниковых   –    Поповых,   и  той атмосферы,   которая формировала их нравственное начало.

      Василий Степанович Каретников – сын  Плёсского  2-ой гильдии  купца  Степана Ивановича  Каретникова и   Александры  Дмитриевны, дочери  Ростовского 1-й гильдии  купца Дмитрия  Алексеевича Хлебникова.  С самого раннего  детства он соприкасался с теми семейными устоями, в которых царило взаимопонимание, уважение  и любовь к ближнему.  Огромное влияние оказывала и Православная Церковь,  приход  которой находился, как правило, напротив особняка.
      `,

      `
      Строительство храма проходило в несколько этапов. В 1779 году на средства помещика, Надворного Советника Андрея Ивановича
      Хметевского вместо старой деревянной церкви был сооружён одноэтажный тёплый храм в честь Происхождения честных древ Животворящего Креста Господня с придельным престолом во имя Архангела Михаила.
       
      Спустя несколько лет в расположенной неподалёку деревеньке Гридкино случилось чудесное явление Божией Матери. В память об этом событии в 1809 году церковь средствами прихожан обретает второй этаж — холодный храм с престолом во имя иконы Пресвятой Богородицы «Всех скорбящих Радость». Одновременно с этим к храму была пристроена каменная трёхъярусная колокольня.
      В первой половине XIX века с южной стороны колокольни двухэтажная сводчатая палатка, а с северной — крытое крыльцо, ведущее в верхнюю церковь.
      В 1854 году храм становится четырёхпрестольным — в память первого сельского храма на втором этаже тщанием помещицы Натальи Ивановны Чихачёвой был обустроен придел Святителя и Чудотворца Николая.

      Вытянутый равновысокий силуэт здания нарушается лишь четвериком, возвышающимся над абсидой и трапезной на высоту карниза. Оба этажа церкви состоят из практически одинаковых частей: алтаря, непосредственно храма и трапезной. Соответствующие друг другу помещения обоих этажей близки по размерам и практически совпадают в плане, но своды холодного храма существенно выше. На второй этаж ведут два входа: через отдельный вход с северной стороны здания и через помещение нижнего яруса колокольни и трапезной. Для размещения отопительных печей предназначался подвал, расположенный под южной частью трапезной.

      В комплекс также входит одноэтажная кирпичная церковная сторожка, расположенная к северо-западу от Скорбященского храма. Богослужения здесь прекратились в 1937 году, а решением облисполкома от 6 июля 1940 года храм был закрыт и стал использоваться в качестве склада.
     
      Возрождение святыни началось 8 ноября 1998 года освящением престола в честь Казанской иконы Божией Матери на первом этаже храма. К сожалению, страницы истории несколько перепутались, и старинное название во имя иконы «Всех скорбящих Радость» было изменено.
      `
    ],
    link: [
      "https://saints.teykovo.su/objects/berezovik-vseh-skorbyashih-radost-istochnik/",
      "https://saints.teykovo.su/objects/berezovik-arhistratiga-mihaila-istochnik/",
      "http://semyarossii.ru/component/k2/item/312-да-будет-над-ними-пресвятой-покров.html",
      "https://saints.teykovo.su/objects/berezovik-skorbyashenskaya/"
    ]
  },
  {
    id: 2,
    status: false,
    city: 'Богатырёво',
    description: 'Богатырёво',
    img: [
      '/src/components/img/img1-city2.jpg',
      '/src/components/img/img2-city2.jpg',
    ],
    title: [
      'Мемориал Великой Отечественной войны',
      'Церковь Троицы Живоначальной',
    ],
    description_title: [
      ``,

      `
      Старинное село Богатырёво в Тейковской глубинке… Откуда же у него такое красивое название?

      Согласно словарю Брокгауза и Ефрона, слово «богатырь» имеет восточное (тюркское) происхождение. В летописях, описывающих монголо-татарское нашествие, оно упоминается применительно к татарским воеводам в том же смысле, что и «храбор» по отношении к русским воинам. Но с течением времени это слово переносится и на наших храбров, вытесняя древнерусский термин.

      Опираясь на эти данные, можно предположить, что название селению было дано в XIII веке. Возможно именно тогда, в эпоху монголо-татарского ига, и началась история этого поселения.

      Подтверждают эту теорию и народные предания. Согласно им здесь существовала церковь, около который были похоронены семь богатырей. Этот факт и дал название поселению.

      А богатыри тут и действительно могли быть. В расположенной неподалеку деревеньке Алфёровка ханское войско охраняло источник, да и соседний Сахтыш имеет татарское название, которое переводится на русский язык как «гиблое место». Так и сложили здесь семь храбров-богатырей свои головы за Русь-матушку.
      `
    ],
    link: [
      "",
      "https://saints.teykovo.su/objects/bogatyrevo-troickaya/"
    ]
  },
  {
    id: 3,
    status: false,
    city: 'Златоуст',
    description: 'Златоуст',
    img: [
      '/src/components/img/img1-city3.jpg',
      '/src/components/img/img2-city3.jpg',
      '/src/components/img/img3-city3.jpg',
      '/src/components/img/img4-city3.jpg',
    ],
    title: [
      'Купель',
      'Покровское подворье Введенского женского монастыря',
      'Церковь в Златоусте',
      'Церковь Воскресения Христова'
    ],
    description_title: [
      ``,

      `
      Покровское подворье в д. Златоуст Лежневского района было создано в марте 1993 г., в старинной графской усадьбе. Здание усадьбы было восстановленo в течение года. Богослужения в домовой церкви в честь Покрова Пресвятой Богородицы начались в 1995 году на Рождество Христово.
      `,

      `
      Село Златоуст образовалось из Иневежского погоста, расположенного при речке Иневеже(приток р.Ухтохмы). в начале XVII столетия. В погосте имелась деревянная церковь в честь  Иоанна Златоуста (347-407гг.) - Константинопольского архиепископа. Прославился как знаменитый оратор, блестящий талантливый проповедник, за что и прозван Златоустом.

      Златоустовская церковь была построена в 1883 году на средства бывшего члена Святого Синода протоиерея Иоанна Васильевича Рождественского, при ней находилась богадельня для бедных женщин духовного звания. Храм представляет определенный интерес в области архитектуры.  Так, алтарь имеет прямоугольную форму, с небольшой абсидой в центре восточной стены, а также система соединения алтаря с храмом. Снаружи полукруглые стыки, а внутри - остроугольные скосы. Златоустовская церковь как памятник культовой архитектуры выявлена и поставлена на государственный учет в 1973 году.

      В церкви один престол - в честь Иоанна Златоуста. По имени  храма получило свое название и небольшое село, в котором он расположен. Церковь была закрыта в начале 30-х годов и долгое время пустовала. После Великой Отечественной войны в помещении храма находился склад зерна, а в начале 60-х годов помещение переоборудовали под ремонтные мастерские совхоза "Согласие". В результате такого использования помещению храма, его архитектуре был нанесен значительный ущерб. Храм несколько раз подвергался перестройке, были сняты колокола, практически разрушена колокольня. После распада колхоза в 90-е годы  помещение храма было заброшено,  и только совсем недавно  удалось получить разрешение на его восстановление.
      `,

      ``
    ],
    link: [
      "",
      "https://monasterium.ru/monastyri/monastery/pokrovskoe-podvore-vvedenskogo-zhenskogo-monastyrya-g-ivanovo/",
      "https://lezhnevo-r24.gosweb.gosuslugi.ru/o-munitsipalnom-obrazovanii/dostoprimechatelnosti/dostoprimechatelnosti_16.html",
      ""
    ]
  },
  {
    id: 4,
    status: false,
    city: 'Клементьево',
    description: 'Клементьево',
    img: [
      '/src/components/img/img1-city4.jpg',
    ],
    title: [
      'Церковь Спаса Всемилостивого',
    ],
    description_title: [
      `
      В настоящее время утрачены шатровая колокольня, барабан и глава храма; трапезная надстроена деревянным вторым этажом.

      Пример небольшой культовой постройки с традиционной композицией и декором, являющимися традиционными для сакралов севера Владимиро-Суздальских земель.

      Основа храма – двусветный основной объём, покрытый купольной «дутой» кровлей с пологими скатами в основании более крутой кровли (так называемой полицей), к которому примыкает сильно пониженные апсида с высокой пятискатной кровлей и широкая трапезная, пристроенная с противоположной алтарной части стороны к храму. Фасады четверика по краям отмечены лопатками. Арочные окна имеют валиковые бровки. Верхняя часть фасадов отсечена от поля стены карнизом, здесь помещено по три чуть удлиненных дугообразных кокошника. Апсида и трапезная прорезаны окнами, близкими по форме к окнам четверика. Фасады трапезной расчленены лопатками на прясла (по одному проему в каждом). В декоре многократно повторен мотив поребрика: в карнизе, отделяющем кокошники, и в их архивольтах, под бровками окон, в венчающих карнизах трапезной и апсиды (здесь дополнительно включены три ряда пилы). Основной объем перекрыт сомкнутым сводом с узкими диагональными гранями и со световым отверстием барабана, апсида - коробовым сводом, переходящим в граненую конху. На отдалении от самой церкви была построена классическая шатровая колокольня.

      В 30-е годы XX века церковь разрушили: уничтожили шатровую колокольню, барабан и главу храма.

      Во времена коммунистического режима в храме Спаса Всемилостливого и в стоящем недалеко от него доме причта, было обустроено специализированное медицинское учреждение. Здание было перестроено под нужды мед.учреждения, к нему были пристроены многочисленные пристройки из кирпича, возведен второй этаж из бревен. В настоящее время мед.учреждение закрыто, храм находится в весьма неблагоприятном состоянии, не действует.
      `
    ],
    link: [
      "https://lezhnevskoe-r24.gosweb.gosuslugi.ru/o-munitsipalnom-obrazovanii/dostoprimechatelnosti/dostoprimechatelnosti_7.html"
    ]
  },
  {
    id: 5,
    status: false,
    city: 'Озеро Красный остров',
    description: 'Озеро Красный остров',
    img: [
      '/src/components/img/img1-city5.jpg',
      '/src/components/img/img2-city5.jpg',
    ],
    title: [
      'Общий вид',
      'Остров',
    ],
    description_title: [
      `
      Памятник природы Ивановской области "Озеро Красный остров" (далее - ООПТ) (Решение Исполнительного комитета Ивановского областного (промышленного) Совета депутатов трудящихся от 22.02.1965 N 164 "Об охране памятников природы в Ивановской области (Протокол N 5)", Решение Исполнительного комитета Ивановского областного Совета депутатов трудящихся от 27.01.1975 N 2/6 "О порядке признания водных объектов области памятниками природы и передаче их под охрану предприятиям, организациям и учреждениям", решения малого Совета Ивановского областного Совета народных депутатов от 14.07.1993 N 147 "О памятниках природы Ивановской области" и от 14.07.1993 N 148 "Об установлении границ территорий с особым правовым режимом использования земель")

      Озеро Красный остров расположено в Лежневском районе Ивановской области, в 20 км юго-западнее г. Иваново, в 15 км северо-западнее пос. Лежнево, в 8 км восточнее г. Тейково, у юго-восточной окраины д. Красный Остров

      Геологическое строение. Территория памятника природы Ивановской области "Озеро Красный остров" (далее - ООПТ) находится в пределах Московской синеклизы. Кристаллический фундамент платформы сложен породами архея и протерозоя. Его перекрывает мощный чехол палеозойских, мезозойских и кайнозойских осадочных пород. Наиболее древние породы грунтовой толщи - отложения среднего и верхнего карбона. Нижнепермские отложения представлены глинами, песчаниками с небольшими прослойками песков аргиллитов и мергелей. Среднепермские отложения, на которых залегают нижнетриасовые, вскрыты скважиной до глубины 268 м. Верхнеюрские отложения представлены глинами от светло-коричневого до темно-красно-коричневого цветов, а также песчаником серовато-коричневого цвета. Верхние слои дочетвертичных отложений представлены юрскими глинами светло-серого, серого, черного цвета. Четвертичные отложения представлены флювиогляциальными, гляциальными и аллювиальными отложениями. Преобладающими являются ледниковые отложения - конечная морена, суглинки с гравием и галькой, отторженцы крупных дочетвертичных и четвертичных пород, мощностью 1 - 2 м.
      `
    ],
    link: [
      "https://docs.cntd.ru/document/428541774",
      "https://docs.cntd.ru/document/428541774"
    ]
  },
  {
    id: 6,
    status: false,
    city: 'Озеро Рубское',
    description: 'Озеро Рубское',
    img: [
      '/src/components/img/img1-city6.jpg',
    ],
    title: [
      'Общий вид',
    ],
    description_title: [
      `
      Озеро Рубское – прекрасный и удивительный водоем в Ивановской области, настоящая жемчужина средней полосы России.

      Озеро расположено в Тейковском районе в 3 км западнее села Синяя Осока и является самым большим в Ивановском крае. Площадь зеркала – 300 га. Водоем имеет вытянутую с северо-запада на юго-восток форму. Максимальная глубина – 16,2 м, средняя – 4,5 м.

      В окрестностях Рубского озера встречаются 650 видов наземных растений, 60 видов птиц, 20 видов животных. Водная растительность развита слабо. Среди растений водоема наиболее интересен редкий для нашего края вид – полушник шиповатый. В озере обитает 5 видов рыб. На южной границе приозерной территории растет морошка, не характерная для региона, чаще всего ее ягоды не вызревают. Интересными экземплярами флоры Рубского озера являются насекомоядные растения – росянка круглолистая и английская.

      О названии водоема местные жители рассказывают несколько легенд. По одной версии, на месте озера в древности стояло село с рубленой деревянной церковью. Однажды случилась катастрофа, на месте селения образовался провал, поглотивший храм и крестьянские дома. Там, где когда-то жили мирно люди, разлилось большое озеро, названое Рубским в память рубленых храма и изб. Еще одно предание связывает гидроним Рубское с некой битвой (рубкой), произошедшей в древности на озерных берегах.

      Однако все это скорее поэтичные мифы, причудливо отражающие историю. Против первой легенды говорит то, что Рубское озеро древнего ледникового происхождения. Образовалось оно в те исторические времена, когда в его окрестностях не было и не могло быть поселений. Исторические свидетельства более поздних эпох не фиксируют крупных битв вблизи с древним озером. Это лишает оснований и вторую версию толкования гидронима Рубское.

      Если принять во внимание, что в прошлом это название часто писали через букву «п» – Рупское, то возможно, гидроним восходит к древнему славянскому слову «рупа» – яма, котловина, дыра, впадина.

      Тихая водная гладь в окружении болот и лесов привлекает немало людей. Берега озера максимально используются человеком. Только официально здесь действует 12 баз отдыха, не считая неорганизованных туристов. Все это вызывает у экологов тревогу и создает необходимость взять охрану озера под особый контроль.
      `
    ],
    link: [
      "https://iv-obdu.ru/kraevedenie/proekt-samye/sam-bolsh-ozero-ivanov-obl/"
    ]
  },
  {
    id: 7,
    status: false,
    city: 'Озеро Черное',
    description: 'Озеро Черное',
    img: [
      '/src/components/img/img1-city7.jpg',
    ],
    title: [
      'Общий вид',
    ],
    description_title: [
      `
      Чёрное или Таковец — озеро расположено на территории Лежневского района в 14км северо-западнее пос. Лежнево, в 0,7км юго-восточнее д. Аладино, в 1км северо-восточнее д. Таковец, в 3км юго-западнее с. Чернцы. Высота над уровнем моря — 133м.

      Площадь акватории — 10,8га. Максимальная глубина — 20,1 метра, а средняя — 6,7 метра. Объём воды — 0,000723км³.

      Озеро имеет второе название — «Таковец». Потому как «чёрных» озёр в Ивановской области известно несколько. В частности, в Ивановском, Комсомольском, Тейковском, Фурмановском, Южском и в других районах.

      Долина озера выражена слабо, озеро находиться в лесу, поэтому местность просматривается плохо. Озеро окружено заболоченным лесом с преобладанием ольхи чёрной, берёзы, сосны.

      Озеро округлой формы, карстового происхождения, о чём свидетельствуют значительная глубина, слабо выраженная котловина, а также расположенное в 3,8км юго-западнее сходное по генезису озеро Красный Остров.

      Озеро дистрофное, прозрачность воды составляет всего 0,5м. По характеру прибрежной растительности оно полузакрытое. Около 60% протяжённости его берегов покрыты древесно-кустарниковой растительностью.
      `
    ],
    link: [
      "https://ru.ruwiki.ru/wiki/Чёрное_(озеро,_Лежневский_район)"
    ]
  },
  {
    id: 8,
    status: false,
    city: 'Пелгусово',
    description: 'Пелгусово',
    img: [
      '/src/components/img/img1-city8.jpg',
    ],
    title: [
      'Стела',
    ],
    description_title: [
      ``
    ],
    link: [
      ""
    ]
  },
  {
    id: 9,
    status: false,
    city: 'Сахтыш',
    description: 'Сахтыш',
    img: [
      '/src/components/img/img1-city9.jpg',
      '/src/components/img/img2-city9.jpg',
    ],
    title: [
      'Церковь Михаила Архангела',
      'Церковь Николая Чудотворца',
    ],
    description_title: [
      `
      В конце XVIII столетия в пожаре погиб деревянный храм села Сахтыш. С разрешения Епархиального начальства в 1795 году в селе стали строить большую каменную церковь с колокольней. Но из-за недостаточных материальных средств прихожан строительство растянулось на полтора десятка лет. Лишь в 1810 году храм был достроен и освящён в честь Архистратига Божиего Михаила.

      Храм представляет собой высокий двухсветный четверик, увенчанный пятиглавием с центральным световым барабаном. С востока к храму примыкает полукруглая апсида, с запада — трапезная с притвором. В середине столетия была построена каменная ограда.

      Кроме главного престола во имя Михаила Архистратига, здесь же находилось два придела: во имя Святой Троицы и святой великомученицы Екатерины.
      `,

      `
      В 1785 году Епархиальное начальство выдало разрешение на постройку в с. Сахтыш каменных церквей вместо существовавших здесь деревянных.

      Строительство тёплого храма было закончено в 1794 году. С западной стороны к нему примыкала колокольня, вход в которую находился в толще западной стены трапезной. Нижний ярус колокольни одновременно являлся и притвором. В конце XIX века пол храма был выложен цветными кафельными плитками.

      Церковь принадлежит к широко распространённому в Ивановской области типу тёплых храмов. Типичным для них является несоответствие наружного облика и внутреннего объёма.

      Храм закрылся в первой половине XX века. За время запустения была разрушена колокольня, утрачено убранство интерьера.
      `
    ],
    link: [
      "https://saints.teykovo.su/objects/sahtysh-arhangelskaya/",
      "https://saints.teykovo.su/objects/sahtysh-nikolskaya/"
    ]
  },
  {
    id: 10,
    status: false,
    city: 'Хомутово',
    description: 'Хомутово',
    img: [
      '/src/components/img/img1-city10.jpg',
      '/src/components/img/img2-city10.jpg',
      '/src/components/img/img3-city10.jpg',
    ],
    title: [
      'Казанская церковь',
      'Церковная лавка',
      'Церковь Преображения',
    ],
    description_title: [
      `
      Летнюю церковь с колокольней построили в с. Хомутово в 1758 году на средства князя Василия Осиповича Гундорова. Храм был освящён в честь Казанской иконы Божией Матери и имел придел Святителя и Чудотворца Николая.

      15 января 1932 года облисполком вынес решение по закрытию храма. За время запустения он был практически полностью уничтожен. До наших дней дошёл лишь четверик (основной объём). Нет ни алтарной апсиды, ни колокольни, ни трапезной. От былого купола сохранился только металлический каркас с крестом. Полностью уничтожены внутренние отделка и роспись стен.
      `,

      ``,

      `
      Тёплую церковь в Хомутове в честь Преображения Господня построили на средства прихожан в 1868 году.

      В 1936 году богослужения в храме прекратились. Окончательно храм был закрыт 31 июля 1940 года решением облисполкома.
      `
    ],
    link: [
      "https://saints.teykovo.su/objects/homutovo-kazanskaya/",
      "",
      "https://saints.teykovo.su/objects/homutovo-preobrazhenskaya/"
    ]
  },
  {
    id: 11,
    status: false,
    city: 'Чернцы',
    description: 'Чернцы',
    img: [
      '/src/components/img/img1-city11.jpg',
      '/src/components/img/img2-city11.jpg',
    ],
    title: [
      'Центр культуры',
      'Церковь Живоначальной Троицы',
    ],
    description_title: [
      ``,

      `
      Церковь. Действует.
      Престолы: Троицы Живоначальной, Владимирской иконы Божией Матери, Михаила Архангела
      Год постройки: 1780.
      Адрес: Россия, Ивановская область, Лежневский район, с. Чернцы, ул. Центральная, 51

      Проезд: 
      Вариант №1 Ехать из Иваново по шоссе М7 на Суздаль. Свернуть направо по указателю на Ярославль, проехав 3 км от д.Кукарино. Ехать асфальтом разного качества до с. Чернцы 8,1 км. Продолжить движение по главной улице села до храма. Он стоит рядом с дорогой. Общее расстояние от поворота с шоссе М7 - 10,4 км
      Вариант №2 Свернуть с шоссе Иваново - Тейково по указателю на Владимир, Суздаль. Ехать асфальтом хорошего качества. На протяжении всего пути есть только один небольшой подъем. Это подъем после моста через реку Ухтохма. Главная дорога под прямым углом уходит налево. Чернцы остаются за спиной путешественника. Поэтому при подъеме нужно свернуть направо, в Чернцы. Указателей перед перекрестком
      `,
    ],
    link: [
      "",
      "https://sobory.ru/article/?object=35076"
    ]
  },
  {
    id: 12,
    status: false,
    city: 'Шилыково',
    description: 'Шилыково - финал маршрута',
    img: [
      '/src/components/img/img1-city12.jpg',
    ],
    title: [
      'Сергиева пустынь',
    ],
    description_title: [
      `
      Монастырь. Не действует.
      Год основания:приблизительно 2014 - 2016.
      Адрес: Россия, Ивановская область, Лежневский район, в районе с. Стоянцево

      Проезд: Ехать из Иваново по шоссе М7 на Суздаль. Свернуть направо по указателю на Ярославль, проехав 3 км от д.Кукарино. Ехать асфальтом разного качества до с. Чернцы 8,1 км. Свернуть направо по главной дороге и ехать 5 км асфальтом хорошего качества. Пустынь справа в поле, в 300-х м от шоссе.
      `,
    ],
    link: [
      "https://sobory.ru/article/?object=35081"
    ]
  },
])

const doText = (e, id) => {
  isElVisible.value == isElVisible.value.map(x => {
    if (x.id === id)
      x.status = e
    return x
  })
}

const cityTask = ref([
  { id: 0, title: 'Тейково - точка A', status: false },
  { id: 1, title: 'Березовик - точка 1', status: false },
  { id: 2, title: 'Богатырево  - точка 2', status: false },
  { id: 3, title: 'Златоуст - точка 3', status: false },
  { id: 4, title: 'Клементьево - точка 4', status: false },
  { id: 5, title: 'Озеро Красный остров  - точка 5', status: false },
  { id: 6, title: 'Озеро Черное - точка 6', status: false },
  { id: 7, title: 'Озеро Рубское - точка 7', status: false },
  { id: 8, title: 'Пелгусово - точка 8', status: false },
  { id: 9, title: 'Сахтыш - точка 9', status: false },
  { id: 10, title: 'Хомутово - точка 10', status: false },
  { id: 11, title: 'Чернцы - точка 11', status: false },
  { id: 12, title: 'Шилыково - точка B', status: false },
])

const setDoneCity = (id) => {
  cityTask.value == cityTask.value.map(x => {
    if (x.id === id)
      x.status = true
    return x
  })
}

const removeCity = (id) => {
  cityTask.value = cityTask.value.filter(y => y.id !== id)
}

</script>

<style>
ul {
  list-style-type: none;
  /* Убирает буллиты */
}

img {
  max-width: 40%;
  height: auto;
  width: auto\9;
  /* ie8 */
}

p {
  white-space: pre-wrap
}
</style>

<style src="./StoriesCard.scss"></style>
