

Fireworks problem:

TODO:

There is a grid of objects, where fireworks are placed. Every day, one firework can be detonated. There is a potential chain reaction whereby the firework will detonate any other fireworks in its cross (i.e. its like the bombs from bomberman) based off its value. Return the minimum number of days to detonate all fireworks.

```
package main

import (
	"fmt"
	"sort"
)

type Firecracker struct {
	x             int
	y             int
	timeToExplode int
	// blast radius refers to the "+" shaped impact area
	blastRadius int
}

// function to return the min time to detonate all fcs
func fireworksFiasco(firecrackers []Firecracker) int {

	// sort in reverse order of timeToExplode, as in, get the last exploding
	// and manually detonate those first, using dfs to find linked nodes for
	// chain reaction.
	sort.Slice(firecrackers, func(i, j int) bool {
		return firecrackers[i].timeToExplode > firecrackers[j].timeToExplode
	})

	// for a given x coord, get all the fireworks. this way we can look for
	// the ones in the range of the blast radius (y - blastRadius, y + blastRadius)
	xcoordToFCindex := make(map[int][]int)

	// for a given y coord, get all the fireworks. this way we can look for
	// the ones in the range of the blast radius (x - blastRadius, x + blastRadius)
	ycoordToFCindex := make(map[int][]int)
	explodeTimesToFCindex := make(map[int][]int)

	for i, fc := range firecrackers {
		xcoordToFCindex[fc.x] = append(xcoordToFCindex[fc.x], i)
		ycoordToFCindex[fc.y] = append(ycoordToFCindex[fc.y], i)
		explodeTimesToFCindex[fc.timeToExplode] = append(explodeTimesToFCindex[fc.timeToExplode], i)
	}

	for k, _ := range xcoordToFCindex {
		sort.Ints(xcoordToFCindex[k])
	}

	for k, _ := range ycoordToFCindex {
		sort.Ints(ycoordToFCindex[k])
	}

	// kind of like visited
	exploded := make(map[int]bool)
	count := 0

	for i, fc := range firecrackers {

		if exploded[i] {
			continue
		}

		// first, do the autoexplode if any
		fcsExplodingAtThisTime, ok := explodeTimesToFCindex[fc.timeToExplode]
		if ok {

			for i, fcIndex := range fcsExplodingAtThisTime {

				if exploded[fcIndex] {
					continue
				}

				// check those in the same x
				xcoord := firecrackers[fcIndex].x
				fcsInSameX, ok := xcoordToFCindex[xcoord]
				if ok {
					maxY := fc.x + fc.blastRadius
					minY := fc.x - fc.blastRadius
					//use upper and lower bound since fcsInSameX is sorted

					for _, fcInSameXIndex := range fcsInSameX {
						if exploded[fcInSameXIndex] {
							continue
						}

						if firecrackers[fcInSameXIndex].y <= maxY && firecrackers[fcInSameXIndex].y >= minY {
							exploded[fcInSameXIndex] = true
						}
					}
				}

				// check those in the same y
				ycoord := firecrackers[fcIndex].y
				fcsInSameY, ok := ycoordToFCindex[ycoord]
				if ok {
					maxX := fc.y + fc.blastRadius
					minX := fc.y - fc.blastRadius
					for _, fcInSameYIndex := range fcsInSameY {
						if exploded[fcInSameYIndex] {
							continue
						}

						if firecrackers[fcInSameYIndex].x <= maxX && firecrackers[fcInSameYIndex].x >= minX {
							exploded[fcInSameYIndex] = true
						}
					}
				}

				exploded[fcIndex] = true
			}

		}
		// once autoexplode is done, do manual explode
		// find next one that is not exploded

		count++
	}

	return count
}

func main() {

	fcs := []Firecracker{
		{81, 287, 47, 59},
		{81, 118, 25, 40},
		{56, 100, 94, 11},
		{162, 289, 128, 74},
		{11, 245, 37, 6},
		{95, 266, 128, 58},
		{47, 347, 87, 88},
		{390, 215, 141, 8},
		{187, 31, 29, 56},
		{137, 231, 85, 26},
		{13, 290, 194, 63},
		{33, 147, 78, 24},
		{159, 153, 157, 21},
		{389, 199, 0, 5},
		{88, 138, 103, 55},
		{51, 110, 5, 56},
		{266, 228, 161, 2},
		{383, 146, 163, 76},
		{202, 118, 47, 94},
		{377, 263, 196, 20},
		{223, 153, 137, 33},
		{41, 59, 33, 43},
		{291, 2, 78, 36},
		{146, 307, 140, 3},
		{152, 243, 5, 98},
		{225, 151, 115, 57},
		{87, 10, 10, 85},
		{190, 32, 98, 53},
		{191, 182, 184, 97},
		{67, 137, 71, 94},
		{126, 202, 181, 79},
		{66, 70, 93, 86},
		{219, 181, 52, 75},
		{85, 110, 187, 49},
		{328, 18, 184, 3},
		{24, 147, 12, 32},
		{16, 239, 140, 86},
		{251, 76, 40, 51},
		{44, 364, 105, 83},
		{1, 90, 2, 58},
		{167, 31, 178, 54},
		{222, 23, 142, 8},
		{143, 368, 166, 10},
		{135, 40, 104, 62},
		{257, 15, 171, 39},
		{230, 313, 100, 59},
		{320, 383, 70, 84},
		{247, 10, 165, 62},
		{29, 320, 48, 56},
		{95, 266, 0, 56},
		{229, 292, 31, 77},
		{286, 120, 199, 62},
		{247, 292, 88, 11},
		{303, 288, 118, 56},
		{19, 207, 157, 52},
		{275, 181, 53, 95},
		{17, 193, 70, 96},
		{186, 232, 120, 60},
		{322, 229, 61, 60},
		{20, 279, 154, 64},
		{60, 351, 181, 57},
		{316, 200, 39, 37},
		{333, 361, 4, 85},
		{309, 15, 119, 14},
		{240, 262, 140, 0},
		{84, 373, 35, 43},
		{21, 390, 174, 69},
		{70, 336, 138, 72},
		{344, 395, 174, 37},
		{324, 93, 6, 48},
		{152, 220, 22, 71},
		{117, 151, 65, 82},
		{279, 192, 129, 31},
		{321, 55, 111, 43},
		{253, 366, 59, 67},
		{8, 208, 128, 53},
		{374, 284, 175, 74},
		{106, 137, 86, 67},
		{114, 258, 59, 46},
		{123, 324, 187, 57},
		{174, 39, 131, 46},
		{183, 128, 116, 26},
		{277, 212, 36, 51},
		{305, 162, 189, 98},
		{87, 230, 9, 28},
		{359, 61, 2, 18},
		{345, 271, 53, 40},
		{120, 281, 5, 76},
		{309, 266, 156, 95},
		{180, 34, 77, 67},
		{278, 175, 193, 80},
		{208, 231, 65, 58},
		{84, 42, 23, 62},
		{73, 172, 53, 58},
		{327, 96, 48, 13},
		{131, 174, 106, 40},
		{131, 332, 77, 2},
		{54, 283, 130, 86},
		{187, 262, 4, 21},
		{193, 398, 156, 65},
	}

	fmt.Println(fireworksFiasco(fcs))
}

/*
code to generate test cases

	fmt.Println("fcs := []Firecracker{")
	// x, y, timeToExplode, blastRadius
	// 0-400, same, 0 - 200 , 0-100
	for i := 0; i < 100; i++ {
		x := rand.Intn(400)
		y := rand.Intn(400)
		timeToExplode := rand.Intn(200)
		blastRadius := rand.Intn(100)
		fmt.Printf("{%d, %d, %d, %d},\n", x, y, timeToExplode, blastRadius)
	}
	fmt.Println("}")

*/

```