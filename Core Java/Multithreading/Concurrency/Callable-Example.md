```
public class CallabeSearch {

	public static class Search implements Callable<Integer> {
		private List<Integer> integers;
		
		Search(List<Integer> integers) {
			this.integers = integers;			
		}
		
		public Integer call() {
			int max = 0;					
			for(int i = 0; i <= integers.size() - 1; i++) {				
				if(integers.get(i) > max) {
					max = integers.get(i);
				}
			}
			return max;
		}
	}	
	public static void main(String[] args) {		
		List<Integer> integers = getListOfRandomIntegers();
		
		System.out.println(integers);
		
		long startSingle = new Date().getTime();
		System.out.println(linearSearchToFindMax(integers));
		long endSingle = new Date().getTime();
		System.out.println("Time Taken for single threaded: " + (endSingle - startSingle));
		
		long startMultiiple = new Date().getTime();
		ExecutorService executorService = Executors.newFixedThreadPool(2);		
		Search search1 = new CallabeSearch.Search(integers.subList(0, 499));
		Search search2 = new CallabeSearch.Search(integers.subList(500, 999));
		
		Future<Integer> future1 = executorService.submit(search1);
		Future<Integer> future2 = executorService.submit(search2);
		
		try {
			if(future1.get() > future2.get()) {
				System.out.println("Max: " + future1.get());			
			} else {
				System.out.println("Max: " + future2.get());
			}
		} catch(ExecutionException exception) {
			exception.printStackTrace();
		} catch(InterruptedException exception) {
			exception.printStackTrace();
		}
		long endMultiiple = new Date().getTime();
		System.out.println("Time Taken for multi threaded: " + (endMultiiple - startMultiiple));
	}
	
	private static List<Integer> getListOfRandomIntegers() {
		List<Integer> integers = new ArrayList<Integer>(1000);
		Random random = new Random();
		
		for(int i = 0; i < 1000; i++) {
			integers.add(random.nextInt(1000));
		}
		return integers;
	}
	
	private static int linearSearchToFindMax(List<Integer> integers) {
		int max = 0;					
		for(int i = 0; i <= integers.size() - 1; i++) {				
			if(integers.get(i) > max) {
				max = integers.get(i);
			}
		}
		return max;
	}
}
```

Output
```
[488, 484, 221, 313, 835, 297, 68, 928, 412, 985, 443, 194, 485, 937, 229, 592, 475, 640, 226, 421, 195, 651, 280, 508, 999, 61, 695, 110, 220, 724, 462, 393, 131, 511, 341, 466, 11, 11, 616, 730, 272, 213, 188, 774, 154, 154, 601, 728, 868, 66, 468, 947, 590, 466, 152, 732, 530, 689, 977, 989, 992, 538, 620, 179, 94, 392, 702, 815, 384, 833, 912, 929, 256, 497, 540, 207, 777, 15, 46, 86, 662, 740, 282, 552, 874, 808, 798, 843, 219, 174, 99, 867, 617, 376, 614, 317, 477, 949, 509, 644, 23, 839, 296, 185, 744, 201, 334, 195, 280, 549, 409, 910, 853, 876, 367, 687, 274, 87, 661, 718, 519, 330, 746, 924, 594, 328, 270, 492, 218, 18, 726, 870, 564, 808, 420, 462, 205, 522, 887, 675, 554, 472, 588, 276, 974, 478, 624, 141, 65, 731, 659, 79, 562, 649, 282, 733, 489, 471, 594, 130, 779, 609, 580, 680, 459, 729, 113, 196, 466, 7, 587, 974, 970, 996, 733, 468, 877, 684, 184, 341, 981, 938, 412, 435, 247, 677, 375, 506, 313, 424, 213, 973, 548, 192, 628, 847, 472, 142, 610, 103, 123, 132, 29, 477, 142, 596, 335, 970, 804, 500, 492, 132, 776, 246, 474, 214, 122, 420, 628, 142, 165, 657, 978, 351, 912, 970, 905, 535, 191, 923, 123, 971, 5, 94, 226, 47, 496, 958, 150, 786, 337, 785, 400, 13, 671, 396, 858, 908, 951, 273, 774, 325, 618, 708, 80, 838, 3, 987, 528, 667, 491, 555, 536, 277, 587, 175, 430, 662, 566, 44, 486, 208, 624, 872, 552, 445, 710, 64, 961, 545, 907, 633, 985, 660, 653, 214, 784, 292, 994, 176, 269, 736, 962, 492, 253, 247, 594, 221, 84, 206, 794, 363, 443, 856, 76, 796, 247, 728, 345, 358, 426, 706, 618, 278, 984, 783, 800, 683, 807, 871, 936, 524, 804, 41, 335, 888, 654, 990, 253, 684, 209, 140, 409, 878, 634, 982, 57, 321, 186, 592, 124, 601, 713, 665, 23, 894, 984, 881, 80, 534, 666, 858, 930, 299, 824, 315, 821, 948, 112, 718, 905, 70, 97, 307, 887, 227, 502, 990, 852, 355, 396, 260, 531, 695, 954, 635, 86, 717, 476, 599, 793, 597, 652, 736, 595, 985, 61, 849, 457, 291, 261, 260, 857, 785, 495, 576, 520, 300, 826, 813, 48, 919, 226, 22, 2, 834, 865, 892, 188, 853, 33, 868, 455, 402, 385, 31, 335, 867, 49, 992, 759, 763, 891, 330, 17, 905, 48, 967, 648, 6, 124, 261, 314, 207, 152, 530, 501, 31, 946, 521, 852, 676, 427, 957, 53, 49, 397, 978, 387, 196, 974, 443, 276, 670, 677, 669, 462, 992, 280, 371, 402, 397, 120, 235, 349, 802, 73, 318, 87, 529, 330, 932, 98, 221, 461, 741, 929, 760, 588, 909, 658, 840, 625, 47, 914, 337, 591, 882, 963, 612, 242, 297, 580, 100, 688, 147, 61, 433, 75, 667, 174, 22, 380, 243, 3, 28, 549, 897, 974, 754, 362, 396, 521, 516, 133, 903, 998, 752, 101, 731, 693, 880, 539, 260, 41, 753, 761, 258, 679, 674, 543, 719, 236, 576, 235, 480, 770, 934, 980, 133, 31, 818, 748, 122, 283, 963, 159, 568, 971, 46, 156, 902, 407, 952, 71, 960, 924, 566, 536, 634, 734, 408, 236, 926, 806, 196, 293, 873, 308, 638, 73, 227, 986, 797, 676, 685, 556, 889, 763, 277, 719, 537, 790, 861, 341, 257, 265, 530, 522, 784, 568, 616, 631, 759, 164, 795, 976, 797, 798, 872, 724, 944, 414, 298, 865, 175, 416, 528, 65, 970, 884, 203, 365, 555, 929, 78, 236, 421, 918, 846, 264, 202, 413, 793, 845, 156, 315, 227, 479, 521, 664, 595, 271, 481, 872, 92, 337, 579, 107, 935, 701, 211, 695, 142, 80, 825, 272, 211, 535, 427, 522, 447, 928, 762, 43, 55, 596, 17, 903, 137, 981, 458, 472, 292, 560, 204, 578, 157, 758, 271, 41, 622, 317, 415, 616, 177, 390, 518, 503, 842, 603, 324, 848, 706, 343, 146, 974, 704, 449, 189, 146, 842, 550, 13, 819, 721, 283, 917, 561, 874, 428, 365, 511, 385, 4, 962, 611, 128, 537, 264, 50, 526, 819, 366, 189, 586, 185, 271, 114, 222, 255, 385, 937, 857, 800, 438, 356, 413, 501, 40, 889, 119, 935, 634, 343, 644, 870, 401, 275, 976, 518, 369, 406, 442, 43, 108, 332, 132, 906, 669, 212, 863, 507, 275, 927, 515, 382, 129, 543, 731, 321, 930, 741, 311, 763, 985, 895, 99, 416, 695, 484, 365, 250, 406, 405, 204, 200, 218, 898, 844, 541, 519, 190, 309, 32, 462, 201, 403, 220, 25, 920, 129, 963, 854, 66, 55, 44, 40, 953, 170, 885, 528, 612, 490, 567, 363, 773, 943, 45, 613, 115, 485, 336, 411, 326, 630, 563, 158, 539, 270, 205, 603, 259, 410, 864, 576, 332, 90, 813, 865, 283, 957, 162, 80, 4, 364, 66, 395, 161, 871, 295, 999, 307, 539, 726, 563, 663, 125, 294, 519, 688, 640, 759, 267, 773, 562, 164, 428, 862, 892, 60, 105, 25, 745, 978, 100, 555, 814, 959, 372, 861, 175, 937, 935, 469, 43, 26, 892, 973, 405, 800, 910, 989, 708, 372, 909, 664, 764, 417, 807, 341, 547, 91, 548, 309, 800, 330, 743, 899, 749, 233, 32, 365, 965, 903, 214, 150, 600, 706, 146, 493, 668, 98, 774, 413, 838, 553, 885, 978, 374, 213, 100, 997, 416, 880, 510, 44, 239, 21, 709, 577, 972, 774, 164, 597, 916, 686, 850, 529, 999, 544, 272, 73, 957, 787, 956, 550, 43, 810, 382, 790, 99, 660, 391, 969, 162, 133, 306, 955, 834, 7, 667, 121, 912, 729, 43, 234, 192, 793, 142, 395, 548, 81, 43, 591, 916, 508, 810, 650, 823, 388, 445, 344, 247, 609, 893, 62, 795, 695, 61, 860, 422, 685, 451, 398, 492, 301, 75, 158, 253]
999
Time Taken for single threaded: 0
Max: 999
Time Taken for multi threaded: 188
```