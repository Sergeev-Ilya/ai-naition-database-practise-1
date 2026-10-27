## Практическое упражнение - 1

* [business-task.md](https://github.com/Sergeev-Ilya/ai-naition-database-practise-1/blob/main/business-task.md) - первичная формулировка задачи
* [critical-user-journeys.md](https://github.com/Sergeev-Ilya/ai-naition-database-practise-1/blob/main/critical-user-journeys.md) - CUJ
* [elephantAndGoldfish/specReview/next-version.md](https://github.com/Sergeev-Ilya/ai-naition-database-practise-1/blob/main/elephantAndGoldfish/specReview/next-version.md) - предлагаемые* изменения spec после первого ревью.
* [openspec/changes/contact-database/proposal.md](https://github.com/Sergeev-Ilya/ai-naition-database-practise-1/blob/main/openspec/changes/contact-database/proposal.md) - основной spec проекта c sub-spec внутри папки specs. (с внесенными предложениями specReview от E&G)

## Практическое упражнение - 2

* [elephantAndGoldfish/finalReviewers](https://github.com/Sergeev-Ilya/ai-naition-database-practise-1/blob/main/elephantAndGoldfish/finalReviewers/core-agent.md) - core-agent.md промпт для Elephant при ревью, оставльные промпты для суб-агентов при ревью


 При решении задачи использовал только openspec-explore.



## Вот промпты, которые использовал для запуска E&G

1. Ревью Spec

> Запусти пожалуйста ревью спецификации @openspec/changes/contact-database/proposal.md через паттерн Elephant + Goldfish. Для выполнения запроса использую основного агента, которых будет запускать внутри запроса 3 дополнительных суб-агента, ограниченных своей задачей и пустым контекстом (без контекста агента-родителя).

> Итак, 1 суб-агент должен искать лишнее в спецификации. Если что-то найдено - не меняй спецификацию - запиши наблюдения в файл @extra.md

> 2 суб-агент должен искать недостающее и недоспецифицированное в спецификации. Если что-то найдено - не меняй спецификацию - запиши наблюдения в файл @lost.md

> 3 суб-агент должен искать спорные решения в спецификации. Если что-то найдено - не меняй спецификацию - запиши наблюдения в файл @bet.md

> Основной агент родитель должен дождаться окончания работы трех агентов. Проверить появились ли файлы - @extra.md , @lost.md , @bet.md - и если хоть один из них есть - но на их основе создать план исправления спецификации в файле @next-version.md - и перед тем, как его применить - спросить меня в чате насчет этого действия.

> Для основного агента используй выбранную в чате ИИ-модель, для суб-агентов на 1 уровень пониже.  
Пиши коротко и по делу.



————

2. Ревью Code

> Код мы пока не пишем, однако давай заранее подготовим промпты для ревью получившегося кода.

> Я хочу чтобы в папке finalReviewers ты создал по одному .md файлу для каждого суб-агента и 1 .md файл для основного промпта, который планирует вызывать внутри себя всех этих субагентов (в изолированную задачу и без контекста агента-родителя), ждал их завершения их работы, анализировал их выходные файлы и далее составлял свой отсчет на их основе с названием @elephantAndGoldfish/finalReviewers/core-review.md . Промпт для основного агента (файл @elephantAndGoldfish/finalReviewers/core-agent.md ) не изменяет файлы коммита, он лишь создает файл с предупреждениями.

> Итак теперь насчет промптов для суб-агентов:
> 1. Промпт 1-ого суб-агента (файл @elephantAndGoldfish/finalReviewers/clean-code-sub-agent.md ) должен проверить качество написанного кода по Clean Code. Если нашел несоответсвия, не изменяя код, записывать их в файл @elephantAndGoldfish/finalReviewers/clean-code.md .
> 2. Промпт 2-ого суб-агента (файл @elephantAndGoldfish/finalReviewers/adr-sub-agent.md ) должен сделать за выполнением ADR.md в измененных файлах. Если нашел несоответсвия, не изменяя код, записывать их в файл @elephantAndGoldfish/finalReviewers/warning-adr.md .
> 3. Промпт 3-ого субагента (файл @elephantAndGoldfish/finalReviewers/proposal-sub-agent.md ) должен проверить соответствие кода спецификации proposal.md . Если нашел несоответсвия, не изменяя код, записывать их в файл @elephantAndGoldfish/finalReviewers/warning-proposal.md .

> Важное уточнение для промпта главного агента - при вызове сперва мы всегда чистим файлы @warning-proposal.md, warning-adr.md, clean-code.md - чтобы каждое новое ревью делалось с чистого листа.

> Пиши кратко и по делу.