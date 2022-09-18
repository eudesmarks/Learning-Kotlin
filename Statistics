package times

import kotlin.math.*

fun main() {

    val times = mutableListOf<Double>()

    println("Time List (${times.size} times):")
    println(times)
    println("Statistics:")
    println("Best: ${best(times)}")
    println("Worst: ${worst(times)}")
    println("Current Avg of 5: ${currAvgOf(5, times).first} (σ = ${currAvgOf(5, times).second})")
    println("Best Avg of 5: ${bestAvgOf(5, times).first} (σ = ${bestAvgOf(5, times).second})")
    println("Current Avg of 12: ${currAvgOf(12, times).first} (σ = ${currAvgOf(12, times).second})")
    println("Best Avg of 12: ${bestAvgOf(12, times).first} (σ = ${bestAvgOf(12, times).second})")
    println("Current Avg of 50: ${currAvgOf(50, times).first} (σ = ${currAvgOf(50, times).second})")
    println("Best Avg of 50: ${bestAvgOf(50, times).first} (σ = ${bestAvgOf(50, times).second})")
    println("Current Avg of 100: ${currAvgOf(100, times).first} (σ = ${currAvgOf(100, times).second})")
    println("Best Avg of 100: ${bestAvgOf(100, times).first} (σ = ${bestAvgOf(100, times).second})")
    println("Session Avg: ${currAvgOf(times.size, times).first} (σ = ${currAvgOf(times.size, times).second})")
    println("Session Mean: ${mean(times)}")
}

fun best(times: MutableList<Double>): Double {
    return (times.min() * 100.0).roundToInt() / 100.0
}

fun worst(times: MutableList<Double>): Double {
    return (times.max() * 100.0).roundToInt() / 100.0
}

fun removeUncountableTimes(times: MutableList<Double>): MutableList<Double> {
    val x = ceil(times.size.toDouble() * 0.05)
    repeat(x.toInt()) {
        times.remove(times.min())
        times.remove(times.max())
    }
    return times
}

fun calculateAvg(times: MutableList<Double>): Double {
    var i = 0
    var j = times.size
    val listAvgs = mutableListOf<Double>()
    var avg: Double
    var selection: MutableList<Double>
    do {
        selection = times.subList(i, j).toMutableList()
        removeUncountableTimes(selection)
        avg = selection.sum() / selection.size
        listAvgs.add(avg)
        i += 1
        j += 1
    } while (j <= times.size)
    return listAvgs.min()
}

fun calculateStandardDeviation(times: MutableList<Double>): Double {
    val media = times.sum() / times.size
    var soma = 0.0
    for (time in times) {
        soma += abs(time - media).pow(2.0)
    }
    return sqrt(soma / (times.size - 1))
}

fun mean(times: MutableList<Double>): Double {
    return (times.sum() / times.size * 100.0).roundToInt() / 100.0
}

fun currAvgOf(num: Int, times: MutableList<Double>): Pair<Double, Double> {
    val selection = times.subList(times.lastIndex - num + 1, times.lastIndex + 1).toMutableList()
    val avg = (calculateAvg(selection) * 100.0).roundToInt() / 100.0
    val standardDeviation = (calculateStandardDeviation(removeUncountableTimes(selection)) * 100.0).roundToInt() / 100.0
    return Pair(avg, standardDeviation)
}

fun bestAvgOf(num: Int, times: MutableList<Double>): Pair<Double, Double> {
    var i = 0
    var j = num
    val listAvgs = mutableListOf<Double>()
    var selection: MutableList<Double>
    do {
        selection = times.subList(i, j).toMutableList()
        listAvgs.add(calculateAvg(selection))
        i += 1
        j += 1
    } while (j <= times.size)
    val avg = (listAvgs.min() * 100.0).roundToInt() / 100.0
    val indexMin = listAvgs.indexOf(listAvgs.min())
    selection = times.subList(indexMin, indexMin + num).toMutableList()
    val standardDeviation = (calculateStandardDeviation(removeUncountableTimes(selection)) * 100.0).roundToInt() / 100.0
    return Pair(avg, standardDeviation)
}
