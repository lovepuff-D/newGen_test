# newGen_test

Решение:

 // Список курсов
    let courses = [
        {name: "Courses in England", prices: [0, 100]},
        {name: "Courses in Germany", prices: [500, null]},
        {name: "Courses in Italy", prices: [100, 200]},
        {name: "Courses in Russia", prices: [null, 400]},
        {name: "Courses in China", prices: [50, 250]},
        {name: "Courses in USA", prices: [200, null]},
        {name: "Courses in Kazakhstan", prices: [56, 324]},
        {name: "Courses in France", prices: [null, null]},
    ];

    // Варианты цен (фильтры), которые ищет пользователь
    let requiredRange1 = [null, 200];
    let requiredRange2 = [100, 350];
    let requiredRange3 = [200, null];

    function sortByRangeCost(range, arr) {
        //* - означает условно
        console.log(range)
        let startRange = range[0] //Берём начало диапазона
        let endRange = range[1] //Берём конец диапазона

        //Если пользователь выставляет диапозон до *200
        if (startRange === null) {
            //Если у нас минимальная стоимость курса *150 - pass
            //Если у нас минимальная стоимость курса *250 - not pass
            return arr.filter(e => {
                return endRange > e.prices[0]
            })
        }
        //Если пользователь выставляет диапозон от * до бесконечности
        if (endRange === null) {
            return arr.filter(e => {
                //Если у курса стоимость до *бесконечности
                if (e.prices[1] === null) {
                    return true
                }
                return e.prices[1] > startRange
            })
        }
        //Если диапозон двухзначный
        return arr.filter(e => {
            //Если курс стоит от * до бесконечности, то делаем проверку по одному значению, который = *

			//Для курсов у которых от ∞ до ∞
            if (e.prices[0] === e.prices[1]) {
                return e
            }

            if (e.prices[1] === null) {
                //Если курс стоит от * до бесконечности
                return startRange < e.prices[0] && e.prices[0] < endRange
            }
            if (e.prices[0] === null) {
                //Если курс стоит до *
                return startRange < e.prices[1] && e.prices[1] > endRange
            }
            //Еслить ли курсы от *100 до * 200
            return (e.prices[1] < endRange && e.prices[1] > startRange) || (e.prices[0] === e.prices[1])
        })
    }

    function sortByCost(arr) {
        return arr.sort((a, b) => a.prices[0] - b.prices[0])
    }

    console.log(sortByCost(sortByRangeCost(requiredRange3, courses)))
