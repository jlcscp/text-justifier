import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class TextJustify {

	public static String justify(String text, int lineWidth) {

		if (lineWidth >= text.length()) {
			return text;
		}

		List<String> wordsLeft = Arrays.asList(text.split(" "));

		List<String> justifiedText = new ArrayList<>();

		List<String> fittingWords;
		
		while (!(fittingWords = getLineFittingWords(wordsLeft, lineWidth)).isEmpty()) {
			int numberOfSpacesLeft = lineWidth - numberOfOccupiedSpacesByWordsCharacters(fittingWords);
			wordsLeft = wordsLeft.subList(fittingWords.size(), wordsLeft.size());
			if (wordsLeft.size() == 0) {
				justifiedText.add(fittingWords.stream().collect(Collectors.joining(" ")));
			} else {
				justifiedText.add(justifyLine(fittingWords, numberOfSpacesLeft));
			}
		}
		;

		return justifiedText.stream().collect(Collectors.joining("\n"));
	}

	private static int numberOfOccupiedSpacesByWordsCharacters(List<String> fittingWords) {
		return fittingWords.stream().mapToInt(s -> s.length()).sum();
	}

	public static String justifyLine(List<String> lineWords, int numberOfSpacesLeft) {

		if (lineWords.size() <= 1) {
			return lineWords.stream().collect(Collectors.joining(" "));
		}

		int standardNumberOfSpacesBetweenWords = numberOfSpacesLeft / (lineWords.size() - 1);
		int numberOfExtraSpaces = numberOfSpacesLeft % (lineWords.size() - 1);
		String justifiedLine = "";

		for (int wordIndex = 0; wordIndex < lineWords.size(); wordIndex++) {

			String spacesAfterWord;

			if (isLastWord(wordIndex, lineWords.size())) {
				spacesAfterWord = "";
			} else if (isExtraSpaced(wordIndex, numberOfExtraSpaces)) {
				spacesAfterWord = spaces(standardNumberOfSpacesBetweenWords + 1);
			} else {
				spacesAfterWord = spaces(standardNumberOfSpacesBetweenWords);
			}

			justifiedLine += lineWords.get(wordIndex) + spacesAfterWord;

		}

		return justifiedLine;

	}

	public static List<String> getLineFittingWords(List<String> text, int lineWidth) {

		List<String> fittingWords = new ArrayList<>();

		int spacesLeftToFill = lineWidth;

		int wordIndex = 0;
		while (wordsLeft(wordIndex, text) && canFitWord(spacesLeftToFill, text.get(wordIndex))) {
			spacesLeftToFill -= (text.get(wordIndex).length() + 1);
			fittingWords.add(text.get(wordIndex));
			wordIndex++;
		}

		return fittingWords;
	}

	private static boolean wordsLeft(int wordIndex, List<String> text) {
		return wordIndex < text.size();
	}

	private static boolean canFitWord(int spacesLeftToFill, String word) {
		return spacesLeftToFill >= word.length();
	}

	private static boolean isLastWord(int wordIndex, int numberOFWords) {
		return wordIndex == (numberOFWords - 1);
	}

	private static boolean isExtraSpaced(int wordIndex, int remainingUndistributedSpaces) {
		return wordIndex < remainingUndistributedSpaces;
	}

	private static String spaces(int numberOfSpaces) {
		char[] spaces = new char[numberOfSpaces];
		Arrays.fill(spaces, ' ');
		return new String(spaces);
	}

}
