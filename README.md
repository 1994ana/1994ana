const express = require('express');
const cors = require('cors')

const PORT = 3000;

const app = express();

// CORS
// Cross-Origin Resource Sharing
app.use(cors());

// JSON — JavaScript Object Notation
// Нотация объектов JavaScript
// Текстовый формат данных, который после преобразования превращается
// в исполняемый JavaScript

// - JS — 1995
// - AJAX — 2004 (GMail)
//   - JSONP
// - XHR — 2006
// - fetch — 2017

// Способы отправить GET-запрос на сервер с клиента
// - Зайти на страницу по определенному адресу
// - Создать элемент у которого есть src
//   - img
//   - link
//   - script (JavaScript)

const News = Object.seal([
  {
    id: "1",
    // XSS
    // Cross-Site Scripting
    title: "<script>alert(`Конь-людоед в программе «Поле Чудес»`);</script>",
    date: new Date(2024, 9, 2),
    text: "Вчера, не позднее восьми часов вечера, в знаменитой программе «Поле Чудес» появился Конь-людоед. Он был участником первой тройки игроков. В качестве второй тройки выступала группа «Кирпичи». В качестве третьей тройки — группа «NRKTK».",
  },
  {
    id: "2",
    title: "Прошла последняя лекция первого модуля курса по JavaScript",
    date: new Date(2025, 1, 17),
    text: "Сегодня закончилась последняя лекция первого модуля курса Fullstack Frontend разработчик от школы JavaRush. Лектор пришел пьяный. Студенты негодуют.",
  },
]);

app.get("/", function(req, res) {
  res.send("Hello World!");
});

app.get("/news", function(req, res) {
  res.status(200).json(News.map(({ id, title, date, text }) => ({
    id,
    title,
    date: date.toISOString(),
    text,
  })));
});

app.listen(PORT, () => {
  console.log(`Example app listening on port ${PORT}`);
});
