---
title: "Connect Score Board"
slug: connect-score-board
---

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. ~~Do some code organizing and cleanup~~
1. ~~Implement state and shapes~~
1. **Connect each component up to state and reducers**
    1. ~~NextBlock~~
    1. ~~GridBoard~~
    1. ~~Controls~~
    1. ~~Message-Popup~~
    1. **ScoreBoard**
        1. **Implement the `mapStateToProps` function**
        1. **Implement the `mapDispatchToProps` function**
        1. **Connect the `score-board` component and add the actions that it needs**
        1. **Implement the logic for the play/resume buttons**
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

The score board component shows the current score. It also has a play/pause and restart button. The play button should toggle it's text from 'Play' to 'Pause' as the game changes state.

The value displayed for score will come from the game's `state`. The buttons will call actions that play/pause and restart the game.

# Update the ScoreBaord

- Import `connect` from 'react-redux'.
- Import the `pause`, `resume`, `restart` actions.
- Map the `score`, `isRunning`, `gameOver` from state to props.
- Map the `pause`, `resume`, and `restart` actions to the dispatcher.

> [action]
>
> Updated `/src/components/score-board.js`:
>
```js
import React from 'react'
import { useSelector, useDispatch } from 'react-redux'
import { pause, resume, restart } from '../actions'
>
export default function ScoreBoard(props) {
	const dispatch = useDispatch()
	const game = useSelector((state) => state.game)
	const { score, isRunning, gameOver } = game
>
	return (
		<div className="score-board">
			<div>Score:{ score }</div>
			<div>Level: 1</div>
			<button className="score-board-button" onClick={(e) => {
				if (gameOver) { return }
				if (isRunning) {
					dispatch(pause())
				} else {
					dispatch(resume())
				}
			}}>{isRunning ? 'Pause' : 'Play'}</button>
			<button className="score-board-button" onClick={(e) => {
				dispatch(restart())
			}}>Restart</button>
		</div>
	)
}
```
You may have noticed that the past few chapters we've been wiring buttons up, but they aren't doing anything. That's because our game reducers are just returning `state` still!

In the next few chapters, we're going to update those to actually change the state. Our Score Board now **uses Redux/Flux to manage application state!**

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added connection for score board'
$ git push
```
